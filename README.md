# PrivateClaw

[![Status](https://img.shields.io/badge/status-coming%20soon-orange)](https://github.com/privateclaw/privateclaw-core)
[![Platform](https://img.shields.io/badge/platform-Windows-blue)](https://github.com/privateclaw/privateclaw-core)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Based on](https://img.shields.io/badge/based%20on-OpenClaw-purple)](https://github.com/openclawai/openclaw)
[![Privacy](https://img.shields.io/badge/privacy-local%20first-red)](https://github.com/privateclaw/privateclaw-core)

## Don't rent intelligence. Own it.

> The AI industry wants you dependent. Dependent on their APIs, their pricing, their uptime, their terms — and quietly, on their ability to learn from everything you feed them. That's the deal you didn't know you were signing.
>
> You might be paying Microsoft Copilot to summarise your emails and sit inside Teams. Paying OpenAI to run agents that answer customer queries. Paying Otter.ai to transcribe your meetings. Paying Fixer AI, Jasper, or a dozen other single-purpose SaaS tools to automate one task each. Each one feels small. Together, they add up fast — and every single one is built on the same model: you pay monthly, they get smarter, and your data quietly becomes their data.
>
> The compliance exposure is real too. Every time a staff member pastes a customer email into ChatGPT, uploads a contract to a cloud AI tool, or lets an agent read your CRM — you are almost certainly in breach of GDPR. Not in theory. In practice. Data residency, training consent, purpose limitation: the legal risk grows every time you add a new subscription.
>
> But the biggest loss isn't the cost and it isn't even the legal risk — it's the intelligence you're giving away. The AI that knows your business best will win. Your customers, your processes, your pricing, your tone of voice, your institutional knowledge — that's the training data that creates a genuinely useful AI. Right now you're feeding it to someone else's model and renting back a watered-down version of the result.
>
> PrivateClaw gives you the same infrastructure the big players use themselves — because they don't outsource their intelligence, and neither should you. Run open-source models locally. Build agents that know your business inside out. Let your AI get smarter every week from your own data, not theirs. A finance agent that understands your suppliers. An SEO agent that fixes your site the moment it finds a problem. A CRM agent that knows every customer. All of it running on your hardware, under your control, at a fraction of the cost — and improving every single day.
>
> This isn't anti-AI. It's pro-*your*-AI.
>
> Don't rent intelligence. Own it.

---

## Who is PrivateClaw For?

### AI Development Teams
A clean, credential-stripped OpenClaw base with Windows-native tooling. No personal config polluting your foundation. Deploy fast, build on top, stay private.

### Business Owners (Non-Technical)
Just connect Claude Desktop and start a conversation. No developer needed. We are consistently amazed at how a deliberately rough, imperfect prompt still produces outstanding results with Claude Sonnet 4.6 — the model does the heavy lifting so you do not have to.

### AI Enthusiasts
Explore a full agentic business stack on your own hardware. Run powerful local models, experiment with ComfyUI video pipelines, and build your own custom agents on a solid foundation.

---

## Why This Stack Is a Game Changer

The combination of Claude Sonnet 4.6 + Claude Desktop + MCP (Model Context Protocol) represents a step change in what a non-coder can build and operate. MCP is an open standard that lets Claude Desktop connect directly and securely to your live systems — your CRM, your accounting platform, your workflows, your files, your agents — and Sonnet 4.6 reasons across all of them simultaneously, in a single conversation.

This isn't a chatbot. It's a reasoning layer that sits across your entire business stack and can both understand and act.

**A real example from our own business:** Our SEO agent analysed a live WordPress site and produced a world-class technical audit on a par with leading commercial tools like Yoast. But because the WordPress MCP was connected at the same time, the agent didn't just report the issues — it immediately resolved them. Same session, same conversation. No developer. No tickets. No back-and-forth. The outcome we needed, done.

This pattern repeats across every business function the stack covers: finance, CRM, HR, content, job monitoring, transcription, and more. The stack described in this repo is the result of a year of real-world development on a live business — now packaged as a reusable framework so you can get there without starting from scratch.

---

## Core Design Principles

- **Private by default** — local LLMs via Ollama keep routine inference off external APIs. Cloud models (Claude Sonnet 4.6) are used selectively for high-value reasoning tasks only.
- **Low running cost** — the majority of agent work runs on local models at £0/query. External API spend is reserved for tasks that genuinely need frontier intelligence.
- **Your data stays yours** — vector memory, CRM data, documents, and conversation history all live on your own hardware.
- **Non-coder friendly** — Claude Desktop + MCP makes the entire stack operable through natural language. Agents build agents. Claude Desktop writes the config files.
- **Extensible** — the agent tier system scales from a handful of specialists to 25+ named agents handling different business functions.

---

## Hardware Guidance

PrivateClaw runs on low-spec hardware for basic tasks. To run good local models and the full ComfyUI content creation pipeline, you need capable hardware. We are honest about this:

| Hardware Tier | What You Can Run | Approx. Cost |
|---------------|-----------------|-------------|
| Basic (8GB RAM) | Light agents, small models (Phi, Gemma 2B) | Under £500 |
| Mid (16GB RAM, integrated GPU) | Medium models (Llama 3 8B), basic agents | £800 - £1,500 |
| Capable (dedicated GPU, 16GB VRAM) | Full stack, ComfyUI images, good LLMs | £1,500 - £2,500 |
| Full Power | ComfyUI video, large models, full pipeline | £2,500+ |

**Our honest advice: to get real traction with the full PrivateClaw ecosystem, budget upwards of £2,500.**

We advise on and can help source suitable hardware: Mac Mini (M4/M4 Pro), Olares One, Nvidia Spark, Windows NPU/Copilot+ PCs, and custom GPU workstations.

---

## 1. Host Machine Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| OS | Windows 11 | Windows 11 (Dev Mode for advanced features) |
| GPU | NVIDIA 8GB VRAM | NVIDIA RTX 3090 (24GB VRAM) |
| RAM | 32GB | 64GB+ |
| Storage | 1TB SSD | 2TB+ SSD + secondary drive for models/data |
| Docker | Docker Desktop (WSL2) | Docker Desktop (WSL2) |
| Shell | PowerShell 7 | PowerShell 7 |

> Note: The GPU is required for local LLM inference via Ollama and GPU-accelerated speech transcription. A CPU-only build is possible but will be significantly slower.

---

## 2. Stack Architecture

PrivateClaw is organised as four compose stacks sharing a single Docker network. This separation keeps concerns clean, allows individual stacks to be restarted independently, and makes it easy to add or remove capability areas without touching the core stack.

### Shared Network

All stacks attach to `privateclaw-network`. Containers communicate by name (e.g. `http://qdrant:6333`, `http://n8n:5678`).

---

## 3. Stack 1 — Core AI Stack (privateclaw-core)

The foundation layer. Provides local LLM inference, workflow automation, vector memory, search, and media processing.

| Container | Image | Port(s) | Purpose |
|-----------|-------|---------|---------|
| ollama | ollama/ollama | 11434 | Local LLM server — runs open-source models on your GPU |
| open-webui | ghcr.io/open-webui/open-webui | 3000 | Staff-facing chat UI for local model access |
| n8n | n8nio/n8n | 5678 | Workflow automation — the integration backbone |
| postgres | apache/age:PG16 | 5432 | Primary PostgreSQL with graph extension (Apache AGE) |
| qdrant | qdrant/qdrant | 6333, 6334 | Vector database — agent memory and RAG search |
| redis | redis:alpine | 6379 | Cache and message queue |
| searxng | searxng/searxng | 8888 | Private meta-search engine (used by agents for web research) |
| faster-whisper | fedirz/faster-whisper-server | 8001 | GPU-accelerated speech-to-text |
| openwakeword | onerahmet/openai-whisper-asr-webservice | — | Wake word detection for robot/wearable interface |
| ai-interface | custom | 8085 | Interface layer for robot, AI glasses, or wearable device |
| mcpo | ghcr.io/open-webui/mcpo | 8300 | MCP-to-OpenAPI proxy (exposes MCP tools to Open WebUI) |
| comfyui | ghcr.io/ai-dock/comfyui | — | AI image and video generation |
| memgraph | memgraph/memgraph | — | Graph database for relationship mapping |
| watchtower | containrrr/watchtower | — | Automatic container updates (daily) |

> **AI Interface Container:** This container bridges PrivateClaw to physical AI hardware — open-source robotics (e.g. Reachy Mini), AI glasses (e.g. Brilliant Labs Frame), or other wearables. It handles voice input, wake word detection, and routes queries into the agent stack. It can be omitted if you don't have physical hardware.

---

## 4. Stack 2 — Agent Platform (privateclaw-agents)

The intelligence layer. OpenClaw orchestrates named agents, each with their own identity, skills, memory, and access rules.

| Container | Image | Port(s) | Purpose |
|-----------|-------|---------|---------|
| openclaw | openclaw | 18789 (WS) | Multi-agent orchestration gateway |
| openclaw-mcp | ghcr.io/freema/openclaw-mcp | 3005 | MCP bridge — connects OpenClaw to Claude Desktop |
| openclaw-ssl | nginx:alpine | — | SSL termination |
| vault-watcher | custom | — | Monitors markdown vault → auto-chunks to Qdrant for RAG |
| obsidian | custom | 3010 | Knowledge base UI (vault-mounted) |
| minio | minio/minio | 9000, 9001 | Object storage — document drop zone for agents |
| privateclaw-dashboard | nginx:alpine | 8099 | PrivateClaw Control Centre web dashboard |
| privateclaw-dashboard-api | custom | — | Dashboard API backend |

**Agent WebSocket API:**

```
ws://openclaw:18789
Auth: Bearer <YOUR_OPENCLAW_TOKEN>
Method: chat.send → sessionKey: agent:{AGENT_ID}:{SESSION_UUID}
```

---

## 5. Stack 3 — Business Data (privateclaw-data)

Optional but powerful. Hosts your core business datasets with browsing and analytics UIs. The reference build holds a 4.37M record UK company database used for CRM enrichment and prospecting.

| Container | Image | Port(s) | Purpose |
|-----------|-------|---------|---------|
| data-postgres | apache/age:PG16 | 5432 (internal) | Business dataset database |
| data-nocodb | nocodb/nocodb | 8080 | Airtable-style data browser |
| data-metabase | metabase/metabase | 3002 | Analytics and BI dashboards |
| data-pgadmin | dpage/pgadmin4 | 5050 | Postgres admin UI |

---

## 6. Stack 4 — Mission Control (privateclaw-control)

Provides the operational view of the agent platform — health status, doctor reports, agent logs, and infrastructure monitoring.

---

## 7. Stack 5 — Media & Transcription (privateclaw-media)

Handles audio/video download, transcription, and trend monitoring pipelines.

| Container | Port(s) | Purpose |
|-----------|---------|---------|
| whisper-transcriber | 8092 | Whisper transcription service (CPU-optimised for pipeline use) |
| media-roller | 8091 | Media downloader (YouTube, social platforms) |
| media-orchestrator | 8090 | Pipeline orchestrator — coordinates download → transcribe → brief |

---

## 8. Agent Roster

Agents are defined in `openclaw.json` and organised in four tiers. Each agent has a `SOUL.md` (its identity and hard rules), a skills directory, and optionally a memory file. Claude Desktop can talk to any agent via the OpenClaw MCP server.

### Tier 1 — Gateway
| Agent | Role |
|-------|------|
| main | Primary entry point — handles direct chat, routes to routers |

### Tier 2 — Routers
| Agent | Role |
|-------|------|
| platform-router | Routes tasks to the right platform specialist |
| content-router | Routes creative and content tasks |

### Tier 3 — Professional Agents

High-capability agents using frontier or large local models for complex reasoning tasks.

| Agent | Model Tier | Role |
|-------|-----------|------|
| knowledge-pro | Large / frontier | Central RAG maintainer — vault custodian, knowledge indexing |
| crm-priv | Large / frontier | CRM enrichment orchestrator — scores and dispatches research jobs |
| avatar-pro | Large / frontier | AI video and avatar content generation |
| finance-pro | Large / frontier | Finance agent — AR chasing, bill monitoring, reconciliation support |
| hr-pro | Large / frontier | HR agent — connects to your existing HR platform via n8n proxy |

### Tier 4 — Worker / Specialist Agents

Efficient agents using local models (e.g. qwen2.5:14b via Ollama) for high-volume tasks at zero per-query cost.

| Agent | Model | Role |
|-------|-------|------|
| crm-agent | Local | Sole CRM write authority — STOP-and-confirm deduplication protocol |
| enrichment-agent | Local | 5-stage web research pipeline for company/contact enrichment |
| jobs-agent | Local | Daily job board monitor — tracks roles across multiple boards |
| seo-agent | Local | SEO analysis, technical audit, content optimisation |
| ads-agent | Local | Paid advertising management (Google Ads, etc.) |
| wp-agent | Local | WordPress content and technical management via WP MCP |
| content-agent | Local | Content creation, social posts, email copy |
| trend-agent | Local | Social trend discovery — monitors communities for relevant signals |
| transcribe-agent | Local | Routes audio/video content to transcription pipeline |
| doctor | Local | Infrastructure health monitoring — daily reports, container audits |
| general | Local | General-purpose assistant for staff queries |

> **Local model cost:** Tier 4 agents running on qwen2.5:14b or similar via Ollama cost £0 per query. The entire enrichment pipeline, job monitoring, SEO audits, and content drafting run without any API spend. Frontier model spend (Claude Sonnet 4.6) is reserved for Tier 3 tasks that genuinely require deep reasoning.

---

## 9. RAG & Vector Memory

PrivateClaw uses a multi-collection Qdrant setup for agent memory, document retrieval, and shared knowledge.

| Collection | Dimensions | Purpose |
|------------|-----------|---------|
| document_chunks | 768 | General document and file RAG |
| shared_knowledge | 768 | Cross-agent shared business knowledge |
| marketing_docs | 768 | Marketing and brand content |
| seo_content | 768 | SEO knowledge base |
| agent_memory | 1536 | Long-term agent memory |
| crm_knowledge | 768 | CRM platform documentation |
| agent_docs | 768 | Agent operating documentation |

**Embedding model:** nomic-embed-text via Ollama (768d, zero cost)  
**Ingestion:** vault-watcher auto-chunks new `.md` files dropped into the vault  
**Agent access:** Via the QMD (Query Memory & Docs) skill — agents do not query Qdrant directly

---

## 10. MCP Servers (Claude Desktop)

Each MCP server connects Claude Desktop directly to a live system. Claude Sonnet 4.6 can then read from and write to all connected systems in a single conversation.

**Config location:** `%APPDATA%\Claude\claude_desktop_config.json`

| MCP Server | Purpose | Notes |
|------------|---------|-------|
| filesystem | Read/write access to your tools directory | Set paths to your local config directories |
| n8n-mcp | Trigger and manage n8n workflows | Requires your n8n URL and API key |
| crm-mcp | CRM platform access (e.g. GoHighLevel) | Use mcp-remote wrapper — see gotchas below |
| finance-mcp | Accounting platform (e.g. Xero) | Requires Custom Connection app type for machine-to-machine auth |
| openclaw | Direct agent access via SSE | Connects Claude Desktop to your full agent fleet |
| wp-mcp | WordPress site management | Enables agents to read and fix your site directly |
| playwright-mcp | Browser automation | Used by agents for supplier portals and web harvesting |

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem",
               "<YOUR_TOOLS_PATH>", "<YOUR_OPENCLAW_PATH>"]
    },
    "n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "N8N_API_URL": "<YOUR_N8N_URL>",
        "N8N_API_KEY": "<YOUR_N8N_API_KEY>"
      }
    },
    "crm-mcp": {
      "command": "npx",
      "args": ["mcp-remote", "<YOUR_CRM_MCP_URL>"],
      "env": {
        "HEADERS": "{\"Authorization\": \"Bearer <YOUR_CRM_TOKEN>\"}"
      }
    },
    "finance-mcp": {
      "command": "npx",
      "args": ["-y", "@xeroapi/xero-mcp-server@latest"],
      "env": {
        "XERO_CLIENT_ID": "<YOUR_CLIENT_ID>",
        "XERO_CLIENT_SECRET": "<YOUR_CLIENT_SECRET>"
      }
    },
    "openclaw": {
      "type": "sse",
      "url": "<YOUR_OPENCLAW_MCP_URL>"
    }
  }
}
```

> **Critical:** Never use `"type": "http"` for any MCP server entry — this transport type is unsupported and will crash Claude Desktop silently on launch. Always use `mcp-remote` as a stdio proxy wrapper for HTTP/SSE endpoints.

---

## 11. External Integrations

### CRM Platform
- Reference build uses GoHighLevel — any CRM with an MCP or API can be substituted
- One designated agent holds sole write authority with a mandatory confirmation step before any create/update operation
- n8n acts as a proxy layer for agent → CRM calls where direct MCP access is blocked

### Accounting Platform
- Reference build uses Xero via the official Xero MCP server
- **Important:** Create a Custom Connection app type in the Xero developer portal (not Web app) — this enables machine-to-machine auth with offline_access for autonomous token refresh
- Three-layer payment protection: OAuth scope restrictions + DRAFT-only status enforcement + agent SOUL.md hard rules

### Microsoft 365
- Connect via Azure App Registration (n8n credential)
- Enables agents to read/send email, access OneDrive, and interact with Teams

### WhatsApp (Meta)
- Multiple WhatsApp numbers can be registered — one per major channel
- Configure via Meta for Developers → WhatsApp Business API

### Digital Channels (Google / Bing)
- SEO, Ads, and Analytics agents connect via n8n OAuth proxy — agents call internal webhooks, n8n holds all OAuth tokens
- Supports: Google Analytics 4, Google Ads, Google Search Console, Bing Webmaster Tools

### HR Platform
- The hr-pro agent connects to your existing HR system via n8n as a proxy layer
- Any HR platform with an API or OAuth support can be integrated

---

## 12. Cloudflare Tunnel Setup

Cloudflare Tunnel gives your services secure public URLs without opening firewall ports. Install as a Windows service (not a Docker container) so it survives stack restarts.

| Service | Internal URL | Suggested public subdomain |
|---------|-------------|---------------------------|
| n8n | http://localhost:5678 | n8n.<YOUR_DOMAIN> |
| OpenClaw MCP | http://localhost:3005 | openclaw.<YOUR_DOMAIN> |
| Dashboard | http://localhost:8099 | dashboard.<YOUR_DOMAIN> |

> The tunnel allows Claude Desktop (and mobile Claude) to reach your local OpenClaw agents from anywhere, and enables WhatsApp → n8n webhooks to arrive at your stack without port forwarding.

---

## 13. Fresh Build Setup Checklist

### Prerequisites
- [ ] Windows 11, Docker Desktop with WSL2 backend enabled
- [ ] NVIDIA GPU drivers + NVIDIA Container Toolkit
- [ ] Node.js LTS, Python 3.11+, PowerShell 7
- [ ] Claude Desktop installed
- [ ] Cloudflare account + domain

### Install MCP Dependencies
```bash
npm install -g n8n-mcp
npm install -g mcp-remote
```

### Clone and Configure
```bash
git clone https://github.com/privateclaw/privateclaw-core.git
cd privateclaw-core
cp .env.example .env
# Edit .env with your credentials
```

### Start Stacks (in order)
```bash
docker compose -f docker-compose.core.yml up -d
docker compose -f docker-compose.agents.yml up -d
docker compose -f docker-compose.data.yml up -d      # optional
docker compose -f docker-compose.media.yml up -d     # optional
```

### Pull Local Models
```bash
ollama pull qwen2.5:14b          # Primary worker agent model
ollama pull nomic-embed-text     # Embedding model for RAG
ollama pull llama3.2             # General purpose / lightweight
```

### Configure Claude Desktop
- Copy the MCP config template from Section 10
- Replace all `<YOUR_*>` placeholders
- Restart Claude Desktop
- Verify: open Claude Desktop → type "list your connected tools"

### Credentials to Configure
- [ ] CRM platform token and location ID
- [ ] Accounting platform OAuth app (Custom Connection type)
- [ ] n8n API key (generate at `<YOUR_N8N_URL>/settings/api`)
- [ ] M365 Azure app (clientId, tenantId, clientSecret)
- [ ] WhatsApp Meta app tokens
- [ ] Qdrant API key (set in .env, mounted into containers)
- [ ] OpenClaw auth token (set in .env)
- [ ] Cloudflare tunnel token

---

## 14. Known Gotchas

| Issue | Cause | Fix |
|-------|-------|-----|
| Claude Desktop crashes silently on launch | "type": "http" MCP entry in config | Replace with mcp-remote stdio wrapper |
| Claude Desktop crashes before logs are written | CoworkVMService interfering | Disable via registry: HKLM:\SYSTEM\CurrentControlSet\Services\CoworkVMService → Start = 4 |
| Docker CLI not found in PowerShell | Not in PATH | Use full path or add Docker bin dir to PATH |
| Agent config JSON corrupted after write | BOM characters from PowerShell | Use [System.IO.File]::WriteAllText with UTF8Encoding($false) |
| Nested JSON truncated | Default ConvertTo-Json depth | Always use ConvertTo-Json -Depth 20 -Compress |
| Writing to Docker volumes from host | Can't bind-mount to named volume directly | Use alpine container: docker run --rm -v vol:/data alpine sh -c "..." |
| Agent container crash-loops after config edit | Unknown keys in openclaw.json | Only use supported keys: id, name, workspace, model, skills, default, agentDir, heartbeat |

---

## 15. What's in the Repo

```
privateclaw/
├── docker-compose.core.yml        # Stack 1 — Core AI
├── docker-compose.agents.yml      # Stack 2 — Agent Platform
├── docker-compose.data.yml        # Stack 3 — Business Data
├── docker-compose.media.yml       # Stack 5 — Media/Transcription
├── .env.example                   # All required environment variables
├── docs/
│   ├── cloudflare-tunnel-setup.md
│   ├── local-models-guide.md
│   ├── rag-memory-setup.md
│   ├── claude-desktop-mcp-config.md
│   ├── agent-soul-guide.md
│   └── crm-integration-guide.md
├── agents/
│   └── openclaw.json.example      # Agent registry template
├── scripts/
│   └── validate-config.ps1        # Validates openclaw.json schema
└── README.md
```

---

## 🚧 Build Coming Soon

This repository will be populated with the full PrivateClaw stack shortly. Watch this repo to be notified on release.

- GitHub: [github.com/privateclaw](https://github.com/privateclaw)
- Website: [www.totalgroup.co.uk](https://www.totalgroup.co.uk)

---

*PrivateClaw — Private AI infrastructure for businesses that want the power of frontier AI with the privacy and cost control of local deployment.*

*Built by [@privateclaw](https://github.com/privateclaw) · Total Group International · MIT License · Based on OpenClaw*
