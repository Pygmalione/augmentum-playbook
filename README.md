# Operation AUGMENTUM

> Connected Vessels System — Imperium Perseia

## Overview

AUGMENTUM is an integrated AI system designed to serve as an "external prefrontal cortex" for Emperor Karolus of Imperium Perseia. It combines proactive messaging (OpenClaw/Seraphina) with autonomous reasoning (Agent Zero/Zerus) and persistent memory (Graphiti Knowledge Graph).

## Architecture

```
Cesarz Karolus (WhatsApp/Telegram/Voice)
         |
         v
   Seraphina (OpenClaw Master Agent)
    |         |         |         |
    v         v         v         v
  Zerus    Research   Content   Julia
(Agent-0)  Agent     Pipeline  Augusta
    |         |         |         |
    +----+----+----+----+
              |
              v
    Graphiti Knowledge Graph
```

## Documents

| Document | Description |
|----------|-------------|
| [AUGMENTUM-PLAYBOOK.md](AUGMENTUM-PLAYBOOK.md) | Full operational playbook (27KB) |
| [SOUL.md](SOUL.md) | Seraphina persona & rules template |
| [QUICKSTART.md](QUICKSTART.md) | Quick deployment guide |

## Key Features

- **ADHD-optimized communication** — inverted pyramid, max 3 points per message
- **Cross-project context retention** via Graphiti Knowledge Graph
- **Proactive reminders** and daily briefings
- **Automatic task delegation** to specialized agents
- **Multi-channel gateway** — WhatsApp, Telegram, Discord, Voice

## Stack

- **Gateway:** OpenClaw (5 instances on VPS3)
- **Reasoning:** Agent Zero (Zerus)
- **Memory:** Graphiti (Neo4j-based Knowledge Graph)
- **LLM:** CLIProxyAPI (Gemini, Qwen, Claude, DeepSeek)
- **Voice:** Julia Augusta (LiveKit + Inworld TTS)
- **Monitoring:** Grafana + Prometheus + Loki

---

*Imperium Perseia — "Ogarniemy to."*
