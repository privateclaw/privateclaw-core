# PrivateClaw Core

> Your company's first digital employee — a complete private AI ecosystem for business

[![Status](https://img.shields.io/badge/status-coming%20soon-orange)](https://github.com/privateclaw/privateclaw-core)
[![Platform](https://img.shields.io/badge/platform-Windows-blue)](https://github.com/privateclaw/privateclaw-core)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Based on](https://img.shields.io/badge/based%20on-OpenClaw-purple)](https://github.com/openclawai/openclaw)
[![Privacy](https://img.shields.io/badge/privacy-local%20first-red)](https://github.com/privateclaw/privateclaw-core)

---

## What is PrivateClaw?

PrivateClaw is not just an AI tool — it is your company's first **digital employee**.

Built on a credential-free, privacy-hardened fork of [OpenClaw](https://github.com/openclawai/openclaw), PrivateClaw is a complete ecosystem of AI agents, tools and skills designed to run a real business end-to-end. Everything runs **locally on your own hardware**, with your own private models. No data leaves your building. No cloud subscriptions. No API bills.

Whether you are an AI development team looking for a clean private foundation to build on, or a business owner wanting to deploy AI without a technical team, PrivateClaw is designed for both.

---

## The Ecosystem — What PrivateClaw Can Do

PrivateClaw ships as a coordinated suite of specialist agents, each owning a business function:

### Sales & Revenue
- **Lead Generation** — prospecting, outreach sequencing, CRM population
- **Quoting & Proposals** — automated quote generation from templates and pricing data
- **Follow-up & Nurture** — AI-managed pipeline follow-up without human input

### Finance & Admin
- **Finance Admin** — invoice processing, expense categorisation, reporting
- **Document Handling** — contracts, POs, statements processed and filed automatically
- **Scheduling & Coordination** — meeting booking, reminders, task assignment

### Web & Digital Presence
- **Website Building** — AI-generated site content, page creation, CMS management
- **SEO Optimisation** — keyword research, on-page SEO, meta generation, content gap analysis
- **Performance Monitoring** — rankings tracking, analytics reporting, recommendations

### Content Creation
- **Written Content** — blog posts, product descriptions, email campaigns, ad copy
- **Image Generation** — AI-generated visuals via ComfyUI integration
- **Video Generation** — short-form video content production (ComfyUI video pipeline)
- **Social Media Management** — scheduled posting, caption generation, platform optimisation

---

## Who is PrivateClaw For?

### AI Development Teams
A clean, credential-stripped OpenClaw base with Windows-native tooling. No personal config polluting your foundation. Deploy fast, build on top, stay private.

### Business Owners (Non-Technical)
Just connect Claude Desktop and start a conversation. No developer needed. We are consistently amazed at how a deliberately rough, imperfect prompt still produces outstanding results with Claude Sonnet 4.6 — the model does the heavy lifting so you do not have to.

### AI Enthusiasts
Explore a full agentic business stack on your own hardware. Run powerful local models, experiment with ComfyUI video pipelines, and build your own custom agents on a solid foundation.

---

## Hardware Reality Check

OpenClaw runs on low-spec hardware. PrivateClaw will too — for basic tasks.

But to run **good local models** and the full content creation pipeline (including ComfyUI image and video generation), you need capable hardware. We are honest about this:

| Hardware Tier | What You Can Run | Approx. Cost |
|---------------|-----------------|-------------|
| Basic (8GB RAM) | Light agents, small models (Phi, Gemma 2B) | Under £500 |
| Mid (16GB RAM, integrated GPU) | Medium models (Llama 3 8B), basic agents | £800 - £1,500 |
| Capable (dedicated GPU, 16GB VRAM) | Full stack, ComfyUI images, good LLMs | £1,500 - £2,500 |
| Full Power | ComfyUI video, large models, full pipeline | £2,500+ |

**Our honest advice: to get real traction with the full PrivateClaw ecosystem, budget upwards of £2,500.**

### Hardware We Can Recommend or Supply

We advise on and can assist sourcing hardware suited to your budget and use case:

- **Mac Mini (M4/M4 Pro)** — excellent performance per pound, unified memory handles large models well
- **Olares One** — purpose-built private AI home server, clean NAS + compute combo
- **Nvidia Spark** — compact but powerful, ideal for local AI workloads
- **Windows NPU/Memory-Shared Machines** — modern Copilot+ PCs with NPU acceleration, good Windows-native experience
- **Custom GPU Workstations** — for teams needing maximum throughput on ComfyUI and video pipelines

---

## Tech Stack

PrivateClaw integrates a curated set of open-source tools:

| Component | Purpose |
|-----------|---------|
| OpenClaw (base) | Agent orchestration framework |
| Ollama | Local LLM server (Llama, Mistral, Phi, Qwen, etc.) |
| LM Studio | GUI model management and serving |
| ComfyUI | Image and video generation pipeline |
| Claude Desktop | Claude integration via MCP |
| Claude Code | AI-assisted development |
| Docker | Containerised service deployment |
| n8n / Make | Workflow automation connectors |

---

## 🚧 Build Coming Soon

The full PrivateClaw Core build is in active development and will be released here shortly.

**What ships in the first release:**
- Credential-stripped OpenClaw base (no personal data, no hardcoded keys)
- Windows PowerShell setup scripts
- config.template.yaml — clean starting config
- Core business agents: lead gen, quoting, finance admin, content creation
- ComfyUI integration guides for Windows
- Local model configuration for Ollama and LM Studio
- Hardware selection guide

---

## Getting Started Preview

    git clone https://github.com/privateclaw/privateclaw-core.git
    cd privateclaw-core
    python -m venv .venv
    .venv\Scripts\activate
    pip install -r requirements.txt
    copy config.template.yaml config.yaml

Point config.yaml at your local Ollama or LM Studio endpoint. No cloud keys needed.

---

## Stay Updated

Watch this repository to be notified on release.

- GitHub: [github.com/privateclaw](https://github.com/privateclaw)
- Website: [www.totalgroup.co.uk](https://www.totalgroup.co.uk)

---

## License

MIT — see [LICENSE](LICENSE). Based on OpenClaw. Full credit to the original OpenClaw contributors.

---

*Built by [@privateclaw](https://github.com/privateclaw) · Total Group International*
