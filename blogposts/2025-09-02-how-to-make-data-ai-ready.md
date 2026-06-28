# How to make data "AI-ready"? - msandbu.org
The title is a bit misleading, but the main focus is on GenAI applications and services with your data. If you want to build a GenAI service that you want to connect with your data, RAG has so far been the preferred approach. However that does not mean that it is going to be perfect and will always find the most accurate set of data. 

To build an accurate RAG solution, much of the work lies in the preparation of the data. Such as ensuring correct embedding and chucking of the data. How to handle dynamic content and also how metadata is queried through different search mechanisms in the vector store. So many parts that we will take a close look at. 

So in this article, I will dig deeper into 

*   How RAG works – and how it makes data searchable
*   Data chucking 
*   How to build a data pipeline for RAG

So how does RAG actually work? Consider that we want to make a GenAI service that is able to query our data. This is mostly done today using vector stores or vector databases that have some search mechanisms on top. 

Firstly if we want to add our unstructured data such as a document into this vector store we need to do an embedding of the data through an embedding model.  
An embedding is the process of converting text to mathematical vectors, essentially a list of numbers (decimals) that represents something, like a word or a sentence, in a way a computer can understand. 

As an example, consider the following paragraph that we have in a document 

_“We launched Copilot last week and adoption has been stellar. Early metrics show a 32 % drop in ticket volume and a 27 % jump in self-service resolution within the first 48 hours. Finance estimates an annual savings of $1.4 million if the trend holds.”_

Now if we were to embed this paragraph into vectors it could look like something like this. 

**\[0.81, -0.23, 0.45, 0.12, -0.67, 0.94, 0.30, -0.55, 0.76, 0.10\]** which is now a numerical representation of the text above. 

This is a highly simplified example, since if we were to use an embedding model such as OpenAI’s text-embedding-3-small, it would output a **1536-dimensional** vector. 

Without going into too much detail, I want to mention that there are multiple embedding models available from the different providers. Huggingface has an embedding leadership benchmark that shows the strengths and weaknesses of the different embedding models which can be seen here → MTEB Leaderboard – a Hugging Face Space by mteb 

Then these vectors are then stored in a vector store such as Pinecone or Weaviate in addition with the original text. When looking at the data in the vector store it could look like this:

{  
  “id”: “unique-id-123”,  
“values”: \[0.81, -0.23, …, 0.789\],   // the vector (embedding)  
  “metadata”: {  
    “text”: “_We launched Copilot last week and adoption has been stellar…_.”,  
    “source”: “Document A”,  
    “page”: 3  
  }  
}

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/09/image.png?resize=973%2C450&ssl=1)

So when a user wants to ask a question related to the data it will send a prompt/question through the orchestrator (like Langchain/Langgraph/Semantic Kernel) that then sends a request to the vector store using some form of a search method. The search method could return two or more chunks of content that has relevant information, and provide this information back to the LLM that generates an answer to the user. 

### Chunking strategies

Now the issue with this could be if data is chunked the wrong way. Since vector stores cannot store all the original data it has to be split into chunks. The original paragraph could be chucked into two sections like this as an example.

Chunk 1:  
_We launched Copilot last week and adoption has been stellar._ 

Chunk 2:  
_Early metrics show a 32 % drop in ticket volume and a 27 % jump in self-service resolution within the first 48 hours. Finance estimates an annual savings of $1.4 million if the trend holds._

The problem with this approach is that it now loses its original meaning. So If I were to ask about Copilot in the RAG application, the search mechanism would only return the first chuck and not the second one. Since there is no correlation between the two and therefore  not providing me with any context back. This is where chucking strategies come in. How should data be chucked so that I can fit the data into the vector store and still allow it to keep its original meaning in a  RAG engine?

There are different methods depending on which framework you use.

**Fixed-Size Chunking**This method involves dividing text into equal-sized segments, such as 400 words or 800 characters per chunk, regardless of the content.

**Variable-Size Chunking Based on Content**Here, the text is split according to natural boundaries like sentence-ending punctuation, line breaks, or structural cues identified by NLP tools that analyze document layout and meaning.

**Rule-Based Chunking**This approach relies on the document’s intrinsic structure or linguistic boundaries. Typical methods include chunking by sentences or paragraphs, using predefined rules.

**Sliding Window Chunking**This technique produces overlapping chunks by sliding a fixed-size window through the text with a set step size. For example, each chunk may contain 500 words, with the next chunk starting 300 words in—creating a 200-word overlap between chunks.

If we were to have a sliding window or rule based approach here the paragraph would not lose its meaning since both  of the content would be available in the same chunk.  

### RAG data pipeline

Another issue is how to keep this data up to date? Since the original data might be a word document before being embedded into a vector store, therefore If we do not update it regularly it would quickly lose value. Secondly there could  also be documents that we cannot  directly embed such as PDF files, which means we also need  to convert them to a text friendly format so it can be pushed into the vector store. 

Therefore it is also important to build a data pipeline that can automate the process of continuously embedded the vector store with new data from different sources and file types.  

A data pipeline usually consists of the following steps

**1\. Corpus selection and ingestion:**Choose the most relevant data sources and content for your use case.

**2\. Data preprocessing and parsing:  
**Clean and standardise the raw data so it’s ready for embedding and retrieval. A commonly used tool here is markitdown, since it supports PDF, Powerpoint and many other file formats and is able to convert the content to markdown format, which makes it better to structure when chunking. GitHub – microsoft/markitdown: Python tool for converting files and office documents to Markdown.

**3\. Enrichment:**Add helpful metadata to the data and remove any unnecessary or noisy content. Such as adding the title of the document on the top so it will be available in the chunking process. 

**4\. Filtering:**Remove any irrelevant or low-value documents that don’t support your use case.

**5\. Chunking:**Split the cleaned data into smaller, logical sections (“chunks”) for better retrieval performance. The frameworks such as Langchain have different methods to chuck based upon the previous examples, such as LangChain CharacterTextSplitter but this is dependent on which framework you use. 

**6\. Embedding:**Convert each chunk into a vector and store it into a vector store. 

If you plan on using cloud services as the foundation for  RAG application, much of this process can be automated. For instance Azure with AI Search provides a schedule feature that can automatically pull data from a storage account and embed the data on a predefined schedule and put it into Azure AI Search (which is Microsoft cloud based vector store and search service)
