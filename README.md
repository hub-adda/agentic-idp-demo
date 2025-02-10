# Project Setup Guide

This project is built using the LangGraph ReAct Agent Template. Follow the steps below to set up and customize the project.

## Getting Started

### Setup the .env file

1. Create a `.env` file.

```bash
cp .env.example .env
```

2. Define required API keys in your `.env` file.

The primary [search tool](./src/react_agent/tools.py) [^1] used is [Tavily](https://tavily.com/). Create an API key [here](https://app.tavily.com/sign-in).

### Setup the langgraph.json

Ensure your `langgraph.json` file is configured correctly:

```json
{
  "dependencies": [
    ".",
    "agentic_idp_cyberark"
  ],
  "graphs": {
    "agent": "./src/react_agent/graph.py:graph"
  },
  "auth": {
    "path": "agentic_idp_cyberark.auth:auth"
  },
  "env": ".env"
}
```

### Update the pyproject.toml

Ensure your `pyproject.toml` file includes `agentic-idp-cyberark` and install it:

```plaintext
[project]
name = "react-agent"
version = "0.0.1"
description = "Starter template for making a custom Reasoning and Action agent (using tool calling) in LangGraph."
authors = [
    { name = "William Fu-Hinthorn", email = "13333726+hinthornw@users.noreply.github.com" },
]
readme = "README.md"
license = { text = "MIT" }
requires-python = ">=3.11.0,<4.0"

[tool.poetry.dependencies]
langgraph = ">=0.2.6"
langchain-openai = ">=0.3.3"
langchain-anthropic = ">=0.3.0"
langchain-aws = ">=0.2.10"
langchain = ">=0.3.0"
langchain-fireworks = ">=0.2.7"
python-dotenv = ">=1.0.1"
langchain-community = ">=0.3.1"
tavily-python = ">=0.3.1"
agentic-idp-cyberark = {version=">=0.0.1", source="testpypi"}
langgraph-cli = "^0.1.70"
langgraph-api = "^0.0.22"

[[tool.poetry.source]]
name = "testpypi"
url = "https://test.pypi.org/simple/"
priority = "explicit"
```
To update the dependencies [optional], run:
```bash
poetry lock
```

To install the dependencies, run:

```bash
poetry install
```

### Run the LangGraph Server

1. Activate the virtual environment:

   - On macOS/Linux:
     ```bash
     source .venv/bin/activate
     ```
   - On Windows:
     ```bash
     .venv\Scripts\activate
     ```

2. Run the LangGraph command:
   ```bash
   langgraph dev --no-browser
   ```

### Run a Client Using the LangGraph Server

To run a client that interacts with the LangGraph server, follow these steps:

1. Ensure the LangGraph server is running as described in the "Run the Project" section.
2. Create a client script (e.g., `client.py`) to interact with the server. Here is an example using `httpx`:

```python
import httpx

async def main():
    async with httpx.AsyncClient() as client:
        response = await client.post("http://127.0.0.1:8000/your-endpoint", json={"query": "your-query"})
        print(response.json())

if __name__ == "__main__":
    import asyncio
    asyncio.run(main())
```

3. Run the client script:
   ```bash
   python client.py
   ```

### Customize the Project

3. Customize whatever you'd like in the code.
4. Open the folder in LangGraph Studio!

## Tools in the Project

### Search Tool by Tavily

The primary search tool used in this project is Tavily. Tavily provides powerful search capabilities that can be integrated into the ReAct agent to enhance its ability to find and retrieve information.

To use Tavily:

1. Create an API key [here](https://app.tavily.com/sign-in).
2. Add the API key to your `.env` file:

```
TAVILY_API_KEY=your-api-key
```

