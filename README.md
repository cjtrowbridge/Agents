# Agents
A self-hosted agentic pipeline using ollama, jupyter, and autogen.

## Configuration

The agents expect an Ollama server to be running and reachable. Set the
environment variable `OLLAMA_BASE_URL` to the full base URL of your Ollama
instance (for example `http://localhost:11434/v1`). If this variable is not
provided, the notebook defaults to `http://docker-ai:11434/v1`.
