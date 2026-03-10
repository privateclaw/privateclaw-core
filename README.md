# PrivateClaw Core

> **Credential-free OpenClaw fork — optimised for Windows and private AI models**

[![Status](https://img.shields.io/badge/status-coming%20soon-orange)](https://github.com/privateclaw/privateclaw-core)
[![Platform](https://img.shields.io/badge/platform-Windows-blue)](https://github.com/privateclaw/privateclaw-core)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Based on](https://img.shields.io/badge/based%20on-OpenClaw-purple)](https://github.com/openclawai/openclaw)

---

## 🚧 Build Coming Soon

PrivateClaw Core is currently in active development. The full build will be uploaded here shortly.

**What's coming:**
- Complete credential-stripped OpenClaw base (the "Adam" config cleaned of all personal data)
- Windows-native setup scripts (PowerShell, .bat launchers)
- Pre-configured support for local AI models via Ollama and LM Studio
- Clean config templates with no hardcoded keys or personal identifiers
- Windows path handling and environment management fixes
- Getting started guide for non-technical AI enthusiasts on Windows

---

## What is PrivateClaw?

PrivateClaw is a privacy-first, Windows-optimised fork of [OpenClaw](https://github.com/openclawai/openclaw) — a powerful open-source AI agent framework.

The problem PrivateClaw solves: the default OpenClaw "Adam" configuration contains personal credentials, API keys, and personalisation that make it unsuitable for sharing or use as a clean starting point. PrivateClaw strips all of that out to provide a neutral, secure base that anyone can build on top of.

### Key differences from OpenClaw

| Feature | OpenClaw (Adam) | PrivateClaw |
|---------|----------------|-------------|
| Credentials | Hardcoded personal keys | None — clean slate |
| Platform focus | Linux/Mac primary | Windows-first |
| Model support | Cloud APIs default | Local models default |
| Telemetry | Varies | Off by default |
| Starting point | Personal config | Neutral template |

---

## Planned Architecture

    privateclaw-core/
    |-- config.template.yaml     # Clean config — no keys, ready to customise
    |-- setup.ps1                # Windows PowerShell setup script
    |-- requirements.txt         # Python dependencies
    |-- .env.example             # Environment variable template
    |-- agents/                  # Agent definitions (credential-free)
    |-- tools/                   # Tool integrations
    |-- models/                  # Local model connectors
    |   |-- ollama.py            # Ollama integration
    |   |-- lmstudio.py          # LM Studio integration
    |   |-- openai_compat.py     # Any OpenAI-compatible endpoint
    |-- docs/
        |-- windows-setup.md     # Full Windows setup guide
        |-- private-models.md    # Connecting local AI models
        |-- credential-guide.md  # How to add your own keys safely

---

## Quick Preview — Private Model Config

When the build is released, connecting a local model will be as simple as:

    model:
      provider: local
      base_url: http://localhost:11434/v1   # Ollama
      model_name: llama3
      api_key: none

No cloud accounts. No API bills. No data leaving your machine.

---

## Supported Local Model Servers

- **Ollama** — easiest Windows install, runs Llama, Mistral, Phi, Qwen and more
- **LM Studio** — GUI-based, great for non-technical users
- **Any OpenAI-compatible endpoint** — self-hosted vLLM, LiteLLM, Jan, etc.

---

## Why Windows?

Most open-source AI agent frameworks are built and tested on Linux/Mac. Windows users often face:

- Path separator issues (backslash vs forward slash)
- Virtual environment activation differences
- Missing bash/shell script support
- CUDA/GPU setup complexity

PrivateClaw addresses all of these with Windows-native scripts and tested Windows workflows.

---

## Stay Updated

Watch this repository to be notified when the build drops.

- GitHub: [github.com/privateclaw](https://github.com/privateclaw)
- Website: [www.totalgroup.co.uk](https://www.totalgroup.co.uk)

---

## Contributing

Once the initial build is released, contributions are welcome. Please open an issue first to discuss what you would like to change.

---

## License

MIT License — see [LICENSE](LICENSE) for details.

PrivateClaw is a derivative work based on OpenClaw. Full credit to the original OpenClaw contributors.

---

*Built by [@privateclaw](https://github.com/privateclaw) · Total Group International*
