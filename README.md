# Marius Sandbu — Second Brain

This is my public second brain (or even my first useful one?), a living collection of notes, ideas, and knowledge I've built up over time.

## Structure

| Folder | What's in it |
|---|---|
| [`blogposts/`](./blogposts/) | Written articles and blog posts from msandbu.org |
| [`talks/`](./talks/) | Notes and outlines from talks I've given |
| [`waysofthinking/`](./waysofthinking/) | Mental models and thinking patterns |
| [`frameworks/`](./frameworks/) | Conceptual frameworks I use and develop |
| [`me/`](./me/) | About me — values, background, beliefs |

## How to use via MCP

All notes in this repo are automatically vectorized and available through an MCP server at:

```
https://msandbu.no/mcp
```

Connect any MCP-compatible client (Claude, VS Code Copilot, etc.) to that endpoint to semantically search and explore my notes.

### MCP Config example

```json
{
  "servers": {
    "msandbu-second-brain": {
      "url": "https://msandbu.no/mcp",
      "type": "http"
    }
  }
}
```

Available tools:
- **`notes_search`** — semantic search across all notes
- **`notes_list`** — list recent notes by folder/category
- **`notes_get`** — get a specific note by path

## How notes get vectorized

A GitHub Action runs on every push to `main`. Any `.md` file that is added or changed is sent to the Cloudflare Worker, which generates an embedding using Workers AI and stores it in D1. This means the MCP server always reflects the latest state of this repo.

---

Website: [msandbu.no](https://msandbu.no)
