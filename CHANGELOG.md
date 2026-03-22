# Changelog

All notable changes to [Ultimate MCP Client](https://github.com/Dicklesworthstone/ultimate_mcp_client) are documented here.

This project does not use formal versioned releases or tags. The changelog is organized by development phase, with entries grouped by capability area rather than raw diff order. Every entry links to its commit on GitHub.

---

## [Unreleased] -- HEAD

Latest commit: [`454dca0`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/454dca02ffebbc659ebb717d10eaa744012d3484) (2026-03-21)

No unreleased changes beyond the latest documented commit.

---

## Phase 7 -- Project Governance and Infrastructure (2026-01-14 to 2026-02-22)

Project maturation: CI/CD pipelines, licensing, dependency maintenance, and contributor documentation. No new user-facing features.

### Bug Fixes

- Fix Web UI hardcoded `127.0.0.1:8017` -- now dynamically detects host/port from `window.location`, fixing `--port` usage (Fixes #2, #3) ([`d591eef`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/d591eef749eb02ec99544ca4725dc32e551360ff), 2026-01-14)
- Fix `ServerConfig.model_dump()` crash -- replaced with `dataclasses.asdict()` since `ServerConfig` is a `@dataclass`, not a Pydantic model ([`d591eef`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/d591eef749eb02ec99544ca4725dc32e551360ff), 2026-01-14)
- Fix HTTPS/WSS protocol detection and reverse proxy deployments -- prevent mixed-content errors when accessed behind nginx ([`bf025c1`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/bf025c11e9228aff74680ff4b85ed98343fa03c4), 2026-01-14)

### CI / CD

- Add GitHub Actions CI workflow: ruff lint/format, mypy type-check, pytest ([`3e8bf8b`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/3e8bf8b1ba0532b635e36004e11a7be2e8d62e45), 2026-01-17)
- Add release workflow for PyPI publishing via trusted publishing on `v*` tags ([`3e8bf8b`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/3e8bf8b1ba0532b635e36004e11a7be2e8d62e45), 2026-01-17)
- Fix ruff lint CI failures; reformat codebase, migrate deprecated `pyproject.toml` lint config to `[tool.ruff.lint]` ([`4172a55`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/4172a55a383e4f190d61483bd7de9184a4b2b663), 2026-01-23)

### Licensing

- Add MIT License ([`4923196`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/4923196be367165fd0261a92c492c958c260c292), 2026-01-21)
- Upgrade license to MIT with OpenAI/Anthropic Rider restricting use by OpenAI/Anthropic without express written permission ([`ce36e7c`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/ce36e7cf402cf4c69059c314c207689e6e2eb928), 2026-02-21)
- Update README license badge and references to match new license terms ([`823b4b7`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/823b4b73eab06583fbb378bf5f177e88959efc95), 2026-02-22)

### Dependencies

- Bulk-update all Python dependencies to latest stable versions via `uv.lock` refresh ([`16a1b56`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/16a1b56f0563b97b869ba933f0c6b1727ee23b68), 2026-01-18)

### Documentation and Metadata

- Add `AGENTS.md` and `AGENTS_RESEARCH.md` contributor guidance for AI-assisted development ([`ad22f1b`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/ad22f1b580b6f537eb5e010891ed1308c2cabf7b), 2026-01-25)
- Add GitHub social preview image (1280x640 `gh_og_share_image.png`) ([`69aba09`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/69aba09dd942b6029b56764f027474ba2fd16fe8), 2026-02-21)
- Initialize beads issue tracker for dependency-aware task management ([`efbc2dd`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/efbc2dd9b5aedf46ab2d77515b6d86d682b980f2), 2026-02-13)
- Add `.bv/` (beads viewer) to `.gitignore` ([`96c2b2a`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/96c2b2a48c82fe68b944682b95678a9a95dc5312), 2026-02-16)

---

## Phase 6 -- Streaming-HTTP Transport and Stabilization (2025-06-03 to 2025-06-16)

Added the modern `streaming-http` transport protocol, completing the trio of supported transports (`stdio`, `sse`, `streaming-http`).

### Transport Layer

- Add native `streaming-http` transport support via latest FastMCP library for efficient bidirectional HTTP communication ([`a7cb8b4`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/a7cb8b45d0886dc2f26f0efc6d74754aba612c9d), 2025-06-13)
- Implement intelligent transport auto-detection: local file paths become `stdio`, URLs with `/sse` or `/events` become `sse`, general HTTP/HTTPS URLs default to `streaming-http` ([`a7cb8b4`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/a7cb8b45d0886dc2f26f0efc6d74754aba612c9d), 2025-06-13)
- Add `fastmcp` to project dependencies ([`a7cb8b4`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/a7cb8b45d0886dc2f26f0efc6d74754aba612c9d), 2025-06-13)
- Update README to document all three transport types and auto-detection behavior ([`1a08b76`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/1a08b76c7c942903e9f3224ef9cc00b8b0f6beab), 2025-06-13)

### Bug Fixes

- Fix critical connection handling regression in multi-provider client ([`68505e2`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/68505e21ab1c2cf0fe7900d92081ab82fe62252e), 2025-06-14)
- Fix multi-provider client and UI rendering issues ([`6031f5e`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/6031f5e4eb8e9e7add22fa959cc6bb6d04583729), 2025-06-14)
- Fix cross-component issues spanning multi-provider client, multi UI, and robust agent loop ([`fbab193`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/fbab1933a98549a63696ae79a7a5419c56119577), 2025-06-16)
- General multi-provider client stabilization ([`4d7c6f0`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/4d7c6f03f529f5cc5c75f804f0a88bae1134c7f9), 2025-06-03)

---

## Phase 5 -- Robust Agent Loop and Structured Outputs (2025-05-06 to 2025-05-30)

Major rewrite of the agent orchestration layer. The original `agent_master_loop.py` was retired and replaced by `robust_agent_loop.py`, a ground-up reimplementation with structured outputs.

### Agent Orchestration

- Integrate Eidetic Engine agent into the multi-provider client -- massive refactoring of `agent_master_loop.py` (3,488 lines changed) ([`2e1c107`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/2e1c107fe42bb88189fc9746a83a4696e9524937), 2025-05-06)
- Convert agent loop helper functions to Anthropic structured outputs for more reliable tool call parsing ([`c9e1736`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/c9e1736566b9db8def047aa15387c54049ca3fe2), 2025-05-27)
- Add structured outputs throughout Agent Master Loop ([`af8e467`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/af8e467b0b81d2e830b4178370b8c5cb92084012), 2025-05-27)
- Create `robust_agent_loop.py` -- complete rewrite of the agent loop from scratch (2,042 lines) ([`cd0656c`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/cd0656cba4596e34a6cf2618add4d865237d738c), 2025-05-28)
- Iterative integration of robust agent loop into multi-provider client across 8 commits ([`ef7d5df`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/ef7d5df63c2053bccaae7ef77f9a5e1c7ed9b245)...[`2266f6b`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/2266f6b7dbd8583f6a941ef0653da0e065e69654), 2025-05-29)
- Retire `agent_master_loop.py` (renamed to `.pyOLD`); remove unused code from agent loop ([`c9b2201`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/c9b22015b93b11a12c383f14e79bcec27dbcae01), 2025-05-30)

### Multi-Provider Client Enhancements

- Tighten integration between agent loop and UMS (Ultimate MCP Server) tools ([`14b9d39`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/14b9d399b25a0fc554a9c8a55030ee65f884501c)...[`2eb5266`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/2eb52667abcec098d433ac716edbbab4c757e6ec), 2025-05-29)
- Ongoing fixes and improvements to `mcp_client_multi.py` throughout the phase ([`1f68200`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/1f6820013bb99f054cbbc007a7379af0278721b2), 2025-05-13)

### Bug Fixes

- Extensive stabilization across dozens of fix commits through May 2025 (representative: [`9083439`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/9083439ca91d65ab77f8f5f5dcc3542811e7e0fc), [`488544b`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/488544b0bf6f8ca891fe17b661257d0e1c76e34e), [`0f31a35`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/0f31a35f72102644a54d197a238cfcd297b6d2b2), [`f469fdc`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/f469fdc53efb9b5ee8f4a4ab664395f4e47fe9ee))

---

## Phase 4 -- Multi-Provider Client and Responses API (2025-04-24 to 2025-04-29)

Introduced a second, parallel client variant (`mcp_client_multi.py`) with multi-AI-provider support, its own Web UI, and an experimental OpenAI Responses API integration.

### Multi-Provider Client

- Create `mcp_client_multi.py` (7,095 lines) -- a full MCP client supporting multiple AI providers beyond just Anthropic ([`e644cf2`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/e644cf23ef7542c36e393cff9ade3688b8f7ada7), 2025-04-24)
- Add comprehensive server management layer with enhanced connection lifecycle handling ([`26a8682`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/26a86825247b7c34eae2a668361b7111de7c16b2), 2025-04-24)
- Multi-provider client fully working with Anthropic integration ([`06f2971`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/06f2971371429b81247c51ba3fa6f62731858c77), 2025-04-25)
- Add `mcpclientm` CLI entry point for multi-provider variant ([`ed1839d`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/ed1839d92a783d0ef39d644f11f4b27229c01327), 2025-04-25)

### Multi-Provider Web UI

- Create `mcp_client_multi_ui.html` (7,251 lines) -- dedicated Web UI for the multi-provider client ([`439b961`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/439b96133e605f009ead2cbc80ce2a0cacac1b59), 2025-04-25)

### OpenAI Responses API

- Create `mcp_client_multi_with_responses_api.py` -- experimental variant integrating the OpenAI Responses API ([`9107810`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/910781026b337287f517172eb62b2f72d851f4af), 2025-04-29)

### Configuration

- Add `.env-example` with configuration templates for multiple AI providers ([`e644cf2`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/e644cf23ef7542c36e393cff9ade3688b8f7ada7), 2025-04-24)
- Add Cursor IDE rules (`.cursor/rules/`) for project-aware AI coding assistance ([`ed1839d`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/ed1839d92a783d0ef39d644f11f4b27229c01327), 2025-04-25)

### Bug Fixes

- Extensive stabilization of multi-provider server management, connection handling, and UI across 8 commits ([`e50d2dc`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/e50d2dc1fa40efb55a23bac3541ff0337bd5ac3c)...[`843222c`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/843222c991e68b9f592b4eaa261b1d72bc903dfc), 2025-04-24 to 2025-04-29)

---

## Phase 3 -- Agent Master Loop and Eidetic Engine Research (2025-04-13 to 2025-04-23)

Introduced the Agent Master Loop, an autonomous multi-step agent orchestration layer. Also produced the Eidetic Engine research paper exploring novel memory architectures for AI agents.

### Agent Orchestration

- Create `agent_master_loop.py` (1,170 lines) -- alpha implementation of autonomous multi-step tool orchestration ([`6126080`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/6126080da0c26524c33f88887d936a0f9215d784), 2025-04-13)
- Iterative improvements to agent reasoning, tool selection, and error recovery across same-day commits ([`ed6e7ee`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/ed6e7ee4c0dd189715e544d36d67e270456065b4)...[`309abe7`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/309abe73137d3aa2aef89d78897edf1a981e4821), 2025-04-13)
- Next-generation Agent Master Loop with major architectural rework ([`556e2d4`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/556e2d425cd1c9a5603a4410da87eecb2272d863)...[`ebaa7fe`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/ebaa7fea14bdc27c6a80625da0afb014c766ad56), 2025-04-18)

### Research Papers

- Publish `AGENT.md` design document (1,038 lines) and initial Maestro paper (`maestro_paper.md`, 497 lines) ([`1626e34`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/1626e346ee2f4e2cf52dd98b8614dfca7d225e29), 2025-04-13)
- Rename Maestro paper to Eidetic Engine paper (`eidetic_engine_paper.md`) ([`19076bc`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/19076bce4de3b9c14c6a171c934fd02ed168bd38), 2025-04-13)
- Publish Eidetic Engine paper as PDF (multiple revisions) ([`2d3719c`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/2d3719c7c0fc964258ded2e0ad1e9836c68008f9), 2025-04-14; [`f4afea8`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/f4afea819210034b00c0527e489e82cbcdef38ee), 2025-04-18; [`898feb2`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/898feb27f219be0656989ac1f1d86e68eaff7f95), 2025-04-18)
- Add technical analysis document for Agent Master Loop ([`9c87891`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/9c87891718137ae7bd60dee5efd98e7bb757fa31), 2025-04-18)

### Server Connectivity

- Fix SSE transport connection handling ([`e0883d5`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/e0883d52c2b2b48b2cbb6e9bdc4f8024c50c99be), 2025-04-21)
- Improve port scanning detection and mDNS discovery reliability ([`aabe1ec`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/aabe1ec04e36389815933a188333f8d97b20805b), 2025-04-21)

### Bug Fixes

- Major client and UI stability improvements ([`cffee7b`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/cffee7bc44ec5bcc97f94b64cd42789455afc0b5), 2025-04-22)
- Core client resilience improvements ([`f5b5bc2`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/f5b5bc2f7f86dc6dcfa3a64e6a732b4bf7c4497a), 2025-04-23)

---

## Phase 2 -- Web UI, FastAPI Backend, and Packaging (2025-04-09 to 2025-04-12)

Transformed the CLI-only client into a dual-interface application with a full Web UI, REST API backend, and proper Python packaging.

### Web UI

- Create `mcp_client_ui.html` -- single-file reactive Web UI built with Alpine.js, Tailwind CSS, and DaisyUI (1,091 lines initial) ([`5031227`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/5031227aedd05f96704ecb306b2a34c1f1f4ada9), 2025-04-09)
- Web UI working with real-time WebSocket chat streaming ([`ce28a97`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/ce28a97d92adb47e3e23c93d271695ac64b0b401), 2025-04-10)
- Web UI feature-complete: server management modals, tool execution panel, conversation branching tree view, theme switching, settings configuration ([`97a2350`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/97a23504e46307c0c6f7dad89d9361fb4a7fdfcb), 2025-04-10)
- Add DaisyUI theme switching with automatic light/dark code syntax highlighting ([`a935e46`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/a935e463141dc4dd297bcb9a2c2a6829ec2b52d2)...[`0231985`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/0231985050ee93673b38f1606fcc012bd9f420cc), 2025-04-12)
- Enhanced UI: server management modals, visual conversation branching, discovery integration, inline settings panel ([`6a9c678`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/6a9c678144017f92e1c44296392e5d3a31edc03d), 2025-04-11)
- Add screenshots for CLI interactive mode, TUI dashboard, and Web UI ([`8756d0c`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/8756d0caca9d3960d9cb13b68a36168da9658a32)...[`3181ca4`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/3181ca4c58ed3ca3947e3712332665d2928e0796), 2025-04-10)

### FastAPI REST / WebSocket Backend

- Create FastAPI backend with REST API endpoints and WebSocket chat endpoint (`/ws/chat`) for real-time streaming; Uvicorn ASGI server integration ([`5031227`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/5031227aedd05f96704ecb306b2a34c1f1f4ada9)...[`a6b261c`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/a6b261c8ae12a7f49db56a2bdb20c0886df61263), 2025-04-09)
- Add comprehensive REST endpoints: `/api/tools`, `/api/resources`, `/api/prompts`, `/api/conversation/*`, `/api/servers/*`, `/api/tool/execute` (693 lines added) ([`84bf0b2`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/84bf0b2cc10ed7b0748073f7562605320def837c), 2025-04-11)

### CLI Enhancements

- Add `/abort` command to cancel in-progress AI operations ([`5506628`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/550662861fcd6d0eec8e50b7ba2528269a48697a), 2025-04-11)
- Add performance optimizations for CLI rendering ([`0231985`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/0231985050ee93673b38f1606fcc012bd9f420cc), 2025-04-12)

### Python Packaging

- Convert project to installable Python package via Hatchling build system ([`00c134f`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/00c134f1a50740ecc755176dd4001a9ee89aad82), 2025-04-10)
- Add `mcpclient` CLI entry point via `[project.scripts]` in `pyproject.toml` ([`00c134f`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/00c134f1a50740ecc755176dd4001a9ee89aad82), 2025-04-10)
- Add new dependencies: `fastapi`, `uvicorn[standard]`, `websockets`, `python-multipart`, `tiktoken`, `aiofiles`, `opentelemetry-instrumentation` ([`00c134f`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/00c134f1a50740ecc755176dd4001a9ee89aad82), 2025-04-10)

### Server Compatibility

- Validated working integration with Playwright MCP server, proving stdio transport robustness ([`07e6a34`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/07e6a34062dc6a7032d3fe65ebef2a563f24cc8b), 2025-04-11)
- Remove custom SSE client code in favor of upstream MCP SDK's SSE implementation ([`74f44c7`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/74f44c7cdfa5611bc85d8b4d014fb025ed69d1d4), 2025-04-11)

---

## Phase 1 -- Core Client Foundation (2025-04-08 to 2025-04-09)

The initial two-day sprint that built the foundational MCP client from scratch. Established all core subsystems: async MCP protocol handling, CLI interface, conversation management, server discovery, observability, caching, and resilience.

### Core Architecture

- Initial code upload: `mcp_client.py` (1,316 lines), `pyproject.toml` (Python 3.13+, version `1.0.0`), `README.md` ([`1746be4`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/1746be47a6d128a05cc3e62fa91a2e859cff85b9), 2025-04-08)
- Rapid expansion to full async MCP client (~4,000+ lines) with Rich CLI, Typer command framework, and component-based internal architecture (`MCPClient`, `ServerManager`, `ConversationGraph`, `ToolCache`) ([`0945160`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/09451606f487bebbf1252181712b8a40e1971c71)...[`8fc9e2b`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/8fc9e2b37d4d960759f78a49b57970d03df4102f), 2025-04-08)

### STDIO Transport (Key Engineering Effort)

- Implement `RobustStdioSession` -- custom `mcp.ClientSession` for stdio servers with noise filtering (ignores non-JSON-RPC output), direct `asyncio.Future` resolution for responses, and full process lifecycle management ([`ca19a15`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/ca19a15326dc636a8c45f380753399c143fab858), 2025-04-08)
- Implement multi-layered stdout pollution prevention: `StdioProtectionWrapper` (global `sys.stdout` interceptor), `safe_stdout()` context manager, `get_safe_console()` and `safe_print()` utilities -- ensures UI and logging output never corrupt the stdio protocol channel ([`ca19a15`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/ca19a15326dc636a8c45f380753399c143fab858)...[`5ea3478`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/5ea3478965741a77a5d742fde85e3d7fff6f6b20), 2025-04-08)
- Replace upstream MCP client with custom wrapper for stdio transport reliability ([`67041a4`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/67041a4a80d35ba6a84c4add1db7606db343ce86), 2025-04-09)

### Conversation Management

- Implement `ConversationGraph` with `ConversationNode` tree structure -- forkable conversation branches with automatic JSON file persistence ([`8d71e5f`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/8d71e5f2adfdedddbb9981ecb032bab55c528845), 2025-04-08)
- Add `/import` and `/export` CLI commands for conversation branch serialization to portable JSON format ([`7687e6a`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/7687e6a3ec6e6d345e78ba70d491132db32ea3d2), 2025-04-08)

### AI Streaming

- Implement real-time AI response streaming with Rich live rendering in CLI; handle `input_json_delta` events for partial JSON accumulation during tool calls ([`37509d2`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/37509d2a7962ad7170f7739f589e5bb1c1ef5068), 2025-04-08)

### Server Discovery

- Implement filesystem-based stdio server auto-discovery in configurable paths (Python/JS scripts) ([`4d7e993`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/4d7e99384f4d45d5eb4fb9f64ef298aeb6bf495d), 2025-04-08)
- Implement mDNS/Zeroconf LAN discovery (`_mcp._tcp.local.`) with real-time notifications and `/discover` command suite ([`4d7e993`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/4d7e99384f4d45d5eb4fb9f64ef298aeb6bf495d), 2025-04-08)
- Implement remote MCP registry integration for discovering shared servers ([`4d7e993`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/4d7e99384f4d45d5eb4fb9f64ef298aeb6bf495d), 2025-04-08)
- Implement Claude Desktop `claude_desktop_config.json` import with intelligent WSL path adaptation (`adapt_path_for_platform`) and `wsl.exe` command remapping ([`4d7e993`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/4d7e99384f4d45d5eb4fb9f64ef298aeb6bf495d), 2025-04-08)

### Observability

- Integrate OpenTelemetry metrics (request counters, latency histograms, tool execution counts) and distributed tracing (spans) ([`0945160`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/09451606f487bebbf1252181712b8a40e1971c71), 2025-04-08)
- Add live Rich TUI dashboard (`/dashboard` command, `--dashboard` CLI flag) for real-time monitoring of server health, tool usage, and client state ([`0945160`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/09451606f487bebbf1252181712b8a40e1971c71), 2025-04-08)

### Tool Result Caching

- Implement disk-backed (`diskcache`) and in-memory dual-layer tool result cache with configurable TTL per tool category ([`0945160`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/09451606f487bebbf1252181712b8a40e1971c71), 2025-04-08)
- Add cache dependency graph: invalidating one tool's cache (e.g., `weather:current`) automatically invalidates dependents (e.g., `weather:forecast`); viewable via `/cache dependencies` ([`0945160`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/09451606f487bebbf1252181712b8a40e1971c71), 2025-04-08)

### Connection Resilience

- Implement `@retry_with_circuit_breaker` decorator -- automatic retries with exponential backoff; circuit breaker pattern for failing servers ([`0945160`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/09451606f487bebbf1252181712b8a40e1971c71), 2025-04-08)
- Implement `ServerMonitor` -- background health checking with automatic recovery attempts for unresponsive servers ([`0945160`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/09451606f487bebbf1252181712b8a40e1971c71), 2025-04-08)

### Infrastructure

- Add `.gitignore`, `banner.webp` project banner image ([`4d7e993`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/4d7e99384f4d45d5eb4fb9f64ef298aeb6bf495d), [`8d71e5f`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/8d71e5f2adfdedddbb9981ecb032bab55c528845), 2025-04-08)

---

## Key Files Reference

| File | Purpose | Introduced |
|------|---------|------------|
| `mcp_client.py` | Core single-provider MCP client (~10,900 lines; CLI + Web backend) | [`1746be4`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/1746be47a6d128a05cc3e62fa91a2e859cff85b9) (2025-04-08) |
| `mcp_client_ui.html` | Web UI for single-provider client (Alpine.js/DaisyUI, ~9,800 lines) | [`5031227`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/5031227aedd05f96704ecb306b2a34c1f1f4ada9) (2025-04-09) |
| `mcp_client_multi.py` | Multi-provider MCP client variant (~15,700 lines) | [`e644cf2`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/e644cf23ef7542c36e393cff9ade3688b8f7ada7) (2025-04-24) |
| `mcp_client_multi_ui.html` | Web UI for multi-provider client (~9,900 lines) | [`439b961`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/439b96133e605f009ead2cbc80ce2a0cacac1b59) (2025-04-25) |
| `mcp_client_multi_with_responses_api.py` | Experimental OpenAI Responses API variant (~12,300 lines) | [`9107810`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/910781026b337287f517172eb62b2f72d851f4af) (2025-04-29) |
| `robust_agent_loop.py` | Active agent orchestration loop (~4,600 lines) | [`cd0656c`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/cd0656cba4596e34a6cf2618add4d865237d738c) (2025-05-28) |
| `agent_master_loop.py` | Original agent loop (retired, renamed to `.pyOLD`) | [`6126080`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/6126080da0c26524c33f88887d936a0f9215d784) (2025-04-13) |
| `pyproject.toml` | Build config, dependencies, `mcpclient`/`mcpclientm` entry points | [`1746be4`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/1746be47a6d128a05cc3e62fa91a2e859cff85b9) (2025-04-08) |
| `.github/workflows/ci.yml` | CI: lint (ruff), type-check (mypy), test (pytest) | [`3e8bf8b`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/3e8bf8b1ba0532b635e36004e11a7be2e8d62e45) (2026-01-17) |
| `.github/workflows/release.yml` | Release: PyPI publishing on `v*` tags | [`3e8bf8b`](https://github.com/Dicklesworthstone/ultimate_mcp_client/commit/3e8bf8b1ba0532b635e36004e11a7be2e8d62e45) (2026-01-17) |

---

## Project Statistics

| Metric | Value |
|--------|-------|
| Total commits | 151 |
| First commit | 2025-04-08 |
| Latest commit | 2026-03-21 |
| Tags | None |
| Releases | None |
| Version (pyproject.toml) | `1.0.0` (declared, never tagged) |
| Total source lines | ~63,000 across 6 source files |
| License | MIT + OpenAI/Anthropic Rider |

## Contributors

- **Jeffrey Emanuel** ([@Dicklesworthstone](https://github.com/Dicklesworthstone)) -- sole author
