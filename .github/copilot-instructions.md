<!--
Repository-specific Copilot/AI agent guidance for HexStrike
This file is intentionally concise: discovery steps, key commands, and
project-specific notes for agents to be productive quickly.
-->

# Copilot / AI Agent Instructions (HexStrike)

Purpose: Help an AI agent get productive in this repository by pointing to
entrypoints, essential commands, and verified smoke-tests for local dev.

1) Quick discovery steps
- Look for manifests: `package.json`, `pyproject.toml`, `requirements.txt`, `setup.py`, `go.mod`, `Cargo.toml`.
- Entrypoints: search for `hexstrike_mcp.py`, `server`, or `app` under the repo root.
- Dev scripts: check `scripts/`, `Makefile`, and `.github/workflows/`.

2) Build / test / run (local)
- The MCP bridge is started with `hexstrike_mcp.py` (see `mcp.json` in your editor config).
- Local HexStrike base URL (discovered): `http://localhost:8888`
- Health check (verified): `curl -I http://localhost:8888/health`

3) HexStrike discovery (verified during session)
- Base URL: `http://localhost:8888` (from local `mcp.json` / editor MCP config)
- Health endpoint: `http://localhost:8888/health` (returns JSON status and telemetry)

Safe, verified smoke commands:

```bash
curl -I http://localhost:8888/health
nmap -sT -p 8888 localhost
curl --version
```

Tools observed available on the HexStrike server (examples):
- `curl`, `nmap`, `httpx`, `radare2`, `zaproxy`, `sqlmap`, `gdb`, `ghidra`, `msfconsole`.

Notes and cautions
- Tool execution is provided via the MCP bridge (`hexstrike_mcp.py`), not a generic `/execute` HTTP endpoint — prefer using the MCP/stdio bridge when running tools programmatically.
- The health endpoint currently lacks several security response headers (CSP, HSTS, X-Frame-Options, X-Content-Type-Options, X-XSS-Protection); verify before exposing to untrusted networks.
- Avoid destructive scans unless explicitly requested; use `-V`, `--version`, or local-only scans for verification.

4) When in doubt
- Run the health check first, then run a version or `-V` flag for a tool to confirm availability.
- If multiple conflicting patterns exist in the repo, prefer the files under the `hexstrike-ai/` root and `docs/`/`README.md` for authoritative guidance.

---
If you want me to incorporate other repo-specific commands (build/test) into this file, tell me which commands to include and I'll update it.
