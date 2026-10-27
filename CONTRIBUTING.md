# Contributing

## Setup

```sh
git clone https://github.com/dmitthedazed/UIS_MCP.git
cd UIS_MCP
python -m venv .venv && . .venv/bin/activate
pip install -e ".[dev]"
python -m pytest tests/
```

To try your changes against real UIS, export `AIS_USERNAME` and `AIS_PASSWORD` and run `ais-mcp`, or point your MCP client at `.venv/bin/ais-mcp`.

## Adding a tool

1. Write `tool_something()` in the matching file under `src/ais_mcp/tools/`. Get the HTTP session with `get_session()` and the current study and period with `get_context()`.
2. Put HTML parsing in `parsers.py` when it can be reused.
3. Register it in `server.py` with `@app.tool(name="ais_something")`. The docstring is what the agent sees, so say what it returns and what each argument means.
4. If it changes anything in UIS (registers, sends, deletes, submits), say so at the start of the docstring.

## Tests

Tests run without network. Save a piece of real UIS HTML, strip personal data from it, and test the parser on it. Never commit logins, cookies or real names.

## Pull requests

Keep them small. Mention which tools you checked against real UIS.
