<div align="center">

# UIS MCP

MCP server for the STU University Information System ([is.stuba.sk](https://is.stuba.sk), formerly AIS).

Lets Claude, Codex, OpenCode and other MCP clients read your schedule, grades, exams and mail, and act on them.

[![Tests](https://github.com/dmitthedazed/UIS_MCP/actions/workflows/tests.yml/badge.svg)](https://github.com/dmitthedazed/UIS_MCP/actions/workflows/tests.yml)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)

</div>

## Install

Linux, for Claude Code, Codex and OpenCode:

```sh
bash <(curl -fsSL https://gist.githubusercontent.com/dmitthedazed/851024ef40ce538074bdb46e09da8565/raw/install-ais-mcp-linux.sh)
```

Or paste this to your agent:

```text
Install UIS MCP on this machine for my coding agents using
https://gist.github.com/dmitthedazed/851024ef40ce538074bdb46e09da8565
Ask me for my STU login when needed. Never print or commit my password.
```

<details>
<summary>Manual install</summary>

Needs Python 3.11+.

```sh
git clone https://github.com/dmitthedazed/UIS_MCP.git
cd UIS_MCP
python -m venv .venv && . .venv/bin/activate
pip install -e .
```

Add it to your client with your login in the environment, for example in Claude Code:

```sh
claude mcp add uis -e AIS_USERNAME=xlogin -e AIS_PASSWORD=yourpassword -- "$PWD/.venv/bin/ais-mcp"
```

</details>

## What it can do

| Area | Tools |
| --- | --- |
| Study | grades, study plan progress, course syllabus, grade stats, schoolmates, excuse notes |
| Schedule | timetable, academic calendar, year schedule |
| Exams | list, register, unregister |
| Courses | course registration, lecture sheets, course progress, tests |
| Mail | inbox, read, reply, forward, send, move, delete, attachments |
| Submissions | open submissions, file upload, thesis topics |
| Documents | documents, noticeboard, print and sealed document requests |
| Finance | fees, scholarships, orders |
| People | search, profile, department contacts |
| Account | who am I, eduroam credentials |

> [!WARNING]
> Some tools change things in UIS for real: registering for exams, sending and deleting mail, submitting files, requesting documents. Keep tool-call confirmation on in your client.

<details>
<summary>Configuration</summary>

All settings are environment variables:

| Variable | |
| --- | --- |
| `AIS_USERNAME` | STU login, e.g. `xlogin` |
| `AIS_PASSWORD` | Password |
| `AIS_DEFAULT_STUDIUM` | Optional. Study ID, skips auto-detection |
| `AIS_DEFAULT_OBDOBI` | Optional. Period ID, skips auto-detection |

</details>

<details>
<summary>Development</summary>

```sh
pip install -e ".[dev]"
python -m pytest tests/
```

Release a new version (bumps, commits, tags and pushes):

```sh
python scripts/bump_version.py patch    # or minor, major, 1.2.3; --no-push to stay local
```

```text
src/ais_mcp/
  server.py     FastMCP server
  session.py    login and HTTP session
  context.py    current study and period detection
  parsers.py    HTML parsing
  tools/        tools grouped by area
```

See [CONTRIBUTING.md](CONTRIBUTING.md).

</details>

## License

[MIT](LICENSE)
