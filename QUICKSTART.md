# AUGMENTUM — Quickstart Guide

> Skrócona instrukcja wdrożenia systemu Connected Vessels

## Krok 1: Audyt OpenClaw na VPS3

```bash
# Zaloguj się na VPS3
ssh root@167.235.117.188

# Sprawdź działające instancje OpenClaw
ps aux | grep openclaw
docker ps | grep openclaw

# Sprawdź konfiguracje
ls -la /root/.openclaw*/
cat /root/.openclaw/openclaw.json
```

## Krok 2: Wybierz instancję dla Seraphiny

Wybierz jedną z 5 instancji jako Seraphina-master.
Skopiuj `SOUL.md` do katalogu agenta:

```bash
cp SOUL.md /root/.openclaw/agents/seraphina/SOUL.md
```

## Krok 3: Skonfiguruj LLM provider

W `openclaw.json` ustaw CLIProxyAPI jako provider:

```json
{
  "models": {
    "providers": [{
      "type": "openai-compatible",
      "baseUrl": "<CLIPROXY_BASE_URL>",
      "apiKey": "<CLIPROXY_API_KEY>",
      "models": ["gemini-3-pro-preview", "qwen3-coder-plus"]
    }]
  }
}
```

## Krok 4: Połącz z Agent Zero

Opcja A — via MCP:
```bash
moltbot mcp add agent-zero http://localhost:<A0_PORT>/mcp
moltbot mcp test agent-zero
```

Opcja B — via A2A:
```json
{
  "integrations": {
    "a2a": {
      "agent-zero": {
        "url": "http://localhost:<A0_PORT>/a2a"
      }
    }
  }
}
```

## Krok 5: Połącz z Graphiti

Skonfiguruj dostęp do Graphiti API:
```json
{
  "integrations": {
    "graphiti": {
      "url": "<GRAPHITI_API_URL>",
      "apiKey": "<GRAPHITI_API_KEY>"
    }
  }
}
```

## Krok 6: Podłącz kanał WhatsApp

W OpenClaw podłącz WhatsApp jako gateway:
```bash
moltbot channel add whatsapp
# Postępuj zgodnie z instrukcjami QR code
```

## Krok 7: Test end-to-end

1. Wyślij wiadomość na WhatsApp: "Seraphina, status projektów"
2. Oczekiwany wynik: Seraphina sprawdza Graphiti i odpowiada ze statusem
3. Wyślij: "Napraw buga X" 
4. Oczekiwany wynik: Seraphina deleguje do Zerusia via A2A

## Krok 8: Ustaw Daily Briefing

Skonfiguruj cron dla poranny briefing o 7:00:
```bash
# W scheduler OpenClaw lub crontab:
0 7 * * * moltbot run seraphina --prompt "Wygeneruj poranny briefing dla Cesarza"
```

---

## Checklist wdrożenia

- [ ] Audyt instancji OpenClaw
- [ ] SOUL.md skopiowany
- [ ] LLM provider skonfigurowany
- [ ] Agent Zero połączony (MCP lub A2A)
- [ ] Graphiti połączony
- [ ] WhatsApp podłączony
- [ ] Test end-to-end przeszedł
- [ ] Daily Briefing cron ustawiony
- [ ] Pierwszy briefing wysłany

---

> Po ukończeniu checklisty — Faza 0 zakończona. Przejdź do Fazy 1 (sekcja 7 w AUGMENTUM-PLAYBOOK.md).
