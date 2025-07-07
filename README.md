# Agents
A self-hosted agentic pipeline using ollama, jupyter, and autogen.

## Configuration

The agents expect an Ollama server to be running and reachable. Set the
environment variable `OLLAMA_BASE_URL` to the full base URL of your Ollama
instance (for example `http://localhost:11434/v1`). If this variable is not
provided, the notebook defaults to `http://docker-ai:11434/v1`.

If the server is unreachable, the notebook may appear to hang while waiting for
model responses. You can verify connectivity by running `curl $OLLAMA_BASE_URL/api/tags`
or by executing the first cell in `agent_notebook.ipynb`, which now checks for
available models before the agents start.

## Logs

Each agent run creates a new subdirectory under `agent_logs` named with a UTC timestamp in the format `Y-m-d-H-M-S-f`. The log markdown file is written as `log.md` inside that folder along with any output files produced by the run.
