# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Google Scholar MCP Server - A Model Context Protocol (MCP) server that enables AI assistants to search and retrieve academic papers from Google Scholar.

## Development Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Or using pyproject.toml
pip install -e .

# Run the MCP server
python google_scholar_server.py
```

## Architecture

The project has a simple two-file structure:

- **google_scholar_server.py**: MCP server using FastMCP. Exposes 3 async tools:
  - `search_google_scholar_key_words`: Basic keyword search
  - `search_google_google_scholar_advanced`: Advanced search with author/year filters
  - `get_author_info`: Retrieve author profile data (affiliation, interests, publications, citations)

- **google_scholar_web_search.py**: Web scraping layer using `requests` + `BeautifulSoup` for Google Scholar HTML parsing, plus `scholarly` library for author data retrieval.

## Key Dependencies

- Python 3.10+
- `mcp[cli]` - MCP server framework
- `scholarly` - Author data retrieval
- `requests` + `bs4` - HTTP requests and HTML parsing

## Configuration for Claude Desktop

Add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "google-scholar": {
      "command": "python",
      "args": ["-m", "google_scholar_mcp_server"]
    }
  }
}
```

Note: The server runs as a module. Either install via `pip install -e .` or adjust the path to point to `google_scholar_server.py` directly.
