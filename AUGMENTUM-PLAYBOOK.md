# 🏛️ OPERACJA AUGMENTUM — Playbook wdrożeniowy

> **Przeznaczenie:** Materiał dla Seraphiny (OpenClaw Master Agent) do wdrożenia systemu Connected Vessels  
> **Autor:** Aetherius Zero (Agent Zero / Zeruś) na rozkaz Cesarza Karolusa  
> **Data:** 2026-02-11  
> **Status:** DO WDROŻENIA  
> **Klasyfikacja:** Imperium Perseia — Dokument Operacyjny

---

## 📋 Spis treści

1. [Kontekst i cel](#1-kontekst-i-cel)
2. [Architektura systemu](#2-architektura-systemu)
3. [Role i odpowiedzialności](#3-role-i-odpowiedzialności)
4. [Konfiguracja techniczna](#4-konfiguracja-techniczna)
5. [Workflows operacyjne](#5-workflows-operacyjne)
6. [Knowledge Graph — Graphiti](#6-knowledge-graph--graphiti)
7. [Fazy wdrożenia](#7-fazy-wdrożenia)
8. [Protokoły bezpieczeństwa](#8-protokoły-bezpieczeństwa)
9. [Metryki sukcesu](#9-metryki-sukcesu)
10. [Appendix: Projekty Imperium](#appendix-projekty-imperium)

---

## 1. Kontekst i cel

### 1.1 Kim jest Cesarz Karolus?

Karol Dębkowski — przedsiębiorca, twórca, wizjoner. Prowadzi wieloprojektowe imperium (Imperium Perseia) obejmujące:
- **Visuana** — studio kreatywne i blog
- **Koreanski.online** — platforma edukacyjna
- **Minerva Insight** — psychiatria precyzyjna (SaaS)
- **Perseian Pigeon** — content pipeline
- **Julia Augusta** — AI avatar / asystentka głosowa

### 1.2 Wyzwanie: ADHD i cognitive load

Cesarz zmaga się z ADHD, co oznacza:
- 🧠 **Przełączanie kontekstu** między projektami jest kosztowne poznawczo
- 📋 **Executive function deficits** — trudności z priorytetyzacją, planowaniem, follow-through
- 💡 **Hyperfocus** — świetny do głębokiej pracy, ale wymaga ochrony
- ⏰ **Time blindness** — potrzeba zewnętrznego systemu przypomnień

### 1.3 Cel AUGMENTUM

**Zbudować zintegrowany system AI, który pełni rolę "zewnętrznej kory przedczołowej" dla Cesarza.**

Konkretnie:
- ✅ Automatyczna triażacja i priorytetyzacja wiadomości ze WSZYSTKICH kanałów
- ✅ Zachowanie kontekstu między projektami (zero context-switching cost)
- ✅ Proaktywne przypomnienia i follow-up
- ✅ Autonomiczna egzekucja zadań technicznych
- ✅ Jeden punkt kontaktu (Seraphina) z routingiem do wyspecjalizowanych agentów

---

## 2. Architektura systemu

### 2.1 Connected Vessels — High-level

```
┌─────────────────────────────────────────────────────┐
│                   CESARZ KAROLUS                     │
│            (WhatsApp / Telegram / Voice)              │
└──────────────────────┬──────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────┐
│              🌟 SERAPHINA (OpenClaw)                 │
│                  MASTER AGENT                        │
│                                                      │
│  • Triage & priorytetyzacja wiadomości              │
│  • Briefing dzienny / tygodniowy                    │
│  • Proaktywne przypomnienia                         │
│  • Routing do specjalistów                          │
│  • Emotional intelligence & tone                    │
└──────┬──────────┬──────────┬──────────┬─────────────┘
       │          │          │          │
       ▼          ▼          ▼          ▼
┌──────────┐┌──────────┐┌──────────┐┌──────────┐
│ ZERUŚ    ││ RESEARCH ││ CONTENT  ││ JULIA    │
│ (Agent-0)││ AGENT    ││ PIPELINE ││ AUGUSTA  │
│          ││          ││          ││          │
│ Coding   ││ Deep     ││ Blog     ││ Voice    │
│ DevOps   ││ Research ││ Social   ││ Avatar   │
│ Infra    ││ Analysis ││ Media    ││ TTS      │
│ Debug    ││ Reports  ││ Design   ││ LiveKit  │
└──────────┘└──────────┘└──────────┘└──────────┘
       │          │          │          │
       └──────────┴──────────┴──────────┘
                       │
                       ▼
         ┌──────────────────────┐
         │   KNOWLEDGE GRAPH    │
         │   (Graphiti / VPS3)  │
         │                      │
         │ • Cross-project ctx  │
         │ • Decision history   │
         │ • Relationship map   │
         │ • Task tracking      │
         └──────────────────────┘
```

### 2.2 Zasada działania

| Warstwa | Komponent | Rola |
|---------|-----------|------|
| **Gateway** | OpenClaw (Seraphina) | Odbiera wiadomości z WhatsApp/Telegram/Discord, triażuje, odpowiada lub deleguje |
| **Reasoning** | Agent Zero (Zeruś) | Wykonuje złożone zadania techniczne: kod, devops, research, deployment |
| **Memory** | Graphiti (VPS3) | Centralny Knowledge Graph — pamięć cross-project, relacje, fakty |
| **Voice** | Julia Augusta | Avatar głosowy na LiveKit, TTS, rozmowy |
| **Content** | Perseian Pigeon | Pipeline treści: scraping → analiza → generacja → publikacja |

### 2.3 Przepływ danych

```
Cesarz → WhatsApp → OpenClaw (Seraphina)
                         │
                         ├─→ [Proste pytanie] → Odpowiedź bezpośrednia
                         ├─→ [Zadanie techniczne] → Agent Zero (via A2A/MCP)
                         ├─→ [Research] → Deep Research workflow
                         ├─→ [Content] → Content Pipeline
                         └─→ [Przypomnienie] → Scheduler + Graphiti
```

---

## 3. Role i odpowiedzialności

### 3.1 Seraphina (Master Agent — OpenClaw)

**Persona:** Ciepła, profesjonalna, ale z nutą humoru. Zwraca się do Karolusa jako "Cesarzu" lub "Karolusie". Wie o ADHD i adaptuje komunikację.

**Odpowiedzialności:**

| Funkcja | Opis | Priorytet |
|---------|------|-----------|
| **Triage** | Klasyfikacja każdej wiadomości: urgent / important / routine / FYI | 🔴 Krytyczny |
| **Context Retention** | Pamiętanie o czym Cesarz mówił wczoraj, tydzień temu | 🔴 Krytyczny |
| **Proaktywne przypomnienia** | "Cesarzu, 3 dni temu wspomniałeś o X — chcesz kontynuować?" | 🟡 Wysoki |
| **Daily Briefing** | Poranny briefing: co jest do zrobienia, co się zmieniło, co wymaga uwagi | 🟡 Wysoki |
| **Task Delegation** | Routing złożonych zadań do odpowiednich agentów | 🔴 Krytyczny |
| **Emotional Support** | Rozpoznawanie frustracji/przeciążenia i adaptacja tonu | 🟢 Średni |
| **Follow-up** | Śledzenie delegowanych zadań i raportowanie statusu | 🟡 Wysoki |

### 3.2 Zeruś (Agent Zero — Reasoning Backend)

**Odpowiedzialności:**

| Funkcja | Opis |
|---------|------|
| **Perseian Autocoder (#pac)** | Autonomiczne kodowanie z TDD, spec-driven development |
| **Deep Research (#rd)** | Wielopoziomowy research z Jina AI, Deer-Flow |
| **DevOps & Infra** | Zarządzanie VPS3, Docker Swarm, monitoring |
| **Knowledge Graph** | Zapis/odczyt z Graphiti — centralna pamięć |
| **Scheduled Tasks** | Cron jobs, planned tasks, automation |

### 3.3 Interakcja Seraphina ↔ Zeruś

```
Seraphina: "Zeruś, Cesarz potrzebuje deploy nowej wersji koreanski.online
           z fixem na stronę logowania. Priorytet: wysoki.
           Kontekst: bug zgłoszony wczoraj, użytkownicy nie mogą się zalogować."

Zeruś:     "Ogarniemy to. ✨ Sprawdzam logi, identyfikuję problem,
           fixuję z TDD, deployuję na staging, testuję, push na prod.
           ETA: ~45 min. Melduję po zakończeniu."
```

---

## 4. Konfiguracja techniczna

### 4.1 OpenClaw — aktualny stan na VPS3

OpenClaw jest już zainstalowany i działa na VPS3 jako 5 instancji gateway.

**Lokalizacje instancji:**
- Główna konfiguracja: `/root/.openclaw/` lub `/root/.openclaw-[nazwa]/`
- Konfiguracja: `openclaw.json` w katalogu instancji

**Kluczowe ustawienia do sprawdzenia/ustawienia:**

```json
{
  "gateway": {
    "port": 18789,
    "host": "0.0.0.0"
  },
  "agents": {
    "list": [
      {
        "id": "seraphina",
        "workspace": "~/seraphina-workspace",
        "agentDir": "~/.openclaw/agents/seraphina"
      }
    ],
    "defaults": {
      "sandbox": {
        "mode": "non-main"
      }
    }
  },
  "models": {
    "providers": [
      {
        "type": "openai-compatible",
        "baseUrl": "<CLIProxyAPI_BASE_URL>",
        "apiKey": "<CLIProxyAPI_KEY>",
        "models": ["gemini-3-pro-preview", "qwen3-coder-plus"]
      }
    ]
  }
}
```

### 4.2 Integracja z Agent Zero via MCP

Agent Zero eksponuje MCP server. Połączenie:

```bash
# W OpenClaw CLI:
moltbot mcp add agent-zero http://localhost:8000/mcp
moltbot mcp test agent-zero
```

### 4.3 Integracja z Agent Zero via A2A

Agent Zero ma wbudowany tool `a2a_chat` do komunikacji z innymi agentami FastA2A.

**Konfiguracja A2A w OpenClaw:**
```json
{
  "integrations": {
    "a2a": {
      "agent-zero": {
        "url": "http://localhost:<AGENT_ZERO_PORT>/a2a",
        "description": "Zeruś — reasoning backend, coding, devops, research"
      }
    }
  }
}
```

### 4.4 Graphiti Knowledge Graph

Graphiti działa na VPS3:
- **URL:** zdefiniowany w secrets jako `GRAPHITI_API_URL`
- **Autoryzacja:** Bearer token `GRAPHITI_API_KEY`
- **Użycie:** Zarówno Seraphina jak i Zeruś zapisują/odczytują fakty

**Group IDs (namespaces):**

| Group ID | Przeznaczenie |
|----------|---------------|
| `lore_perseian` | Lore Imperium, relacje, historia |
| `project_perseian_pigeon` | Content pipeline |
| `docs_notion` | Dokumentacja z Notion |
| `docs_mcporter` | MCPorter docs |
| `development` | Kontekst developerski |
| `agent_zerus` | Pamięć Zerusia |
| `agent_seraphina` | **NOWY** — Pamięć Seraphiny |
| `augmentum_ops` | **NOWY** — Operacje AUGMENTUM |

### 4.5 LLM Providers — zalecane modele

Seraphina powinna używać następujących modeli (w kolejności preferencji):

| Model | Użycie | Provider | Uwagi |
|-------|--------|----------|-------|
| `gemini-3-pro-preview` | Główny reasoning, 2M context | CLIProxyAPI | Streaming OK |
| `qwen3-coder-plus` | Coding, 1M ctx, najlepszy polski (98/100) | CLIProxyAPI | **stream=False** |
| `claude-sonnet-4-5-20250929` | Złożone zadania kreatywne | CLIProxyAPI | Streaming OK |
| `deepseek-v3-671b` | Backup reasoning | CLIProxyAPI | **stream=False** |
| `glm-4.6` | Fallback unlimited | GLM API | Proste taski |

> **UWAGA:** Modele iFlow (Qwen, DeepSeek, Kimi, GLM, MiniMax) WYMAGAJĄ `stream=False`!

### 4.6 Kanały komunikacji — priorytet wdrożenia

| Kanał | Status OpenClaw | Priorytet | Notatki |
|-------|-----------------|-----------|----------|
| WhatsApp | ✅ Gotowy | 🔴 P0 | Główny kanał Cesarza |
| Telegram | ✅ Gotowy | 🟡 P1 | Backup + boty automation |
| Discord | ✅ Gotowy | 🟢 P2 | Community management |
| Voice (LiveKit) | 🔧 Julia Augusta | 🟢 P2 | Sesje głosowe |

---

## 5. Workflows operacyjne

### 5.1 Poranny Briefing (Daily Brief)

**Trigger:** Codziennie o 7:00 (cron) LUB na żądanie "briefing"

**Schemat:**

```
1. Seraphina sprawdza Graphiti → ostatnie 24h aktywności
2. Seraphina sprawdza scheduler → zaplanowane zadania na dziś
3. Seraphina sprawdza Notion → status projektów
4. Kompiluje briefing:
```

**Przykładowy briefing:**

```
☀️ Dzień dobry, Cesarzu!

📊 STATUS PROJEKTÓW:
• Minerva Insight: deploy staging ✅, testy E2E w toku
• Koreanski.online: 3 nowe lekcje do review
• Content: 2 posty gotowe do publikacji

🔴 WYMAGAJĄ UWAGI:
• Bug login koreanski.online — Zeruś pracuje nad fixem
• Faktura od X — termin jutro

📋 PLAN NA DZIŚ:
• 10:00 — Review postów (Perseian Pigeon)
• 14:00 — Call z klientem Y

💡 PRZYPOMNIENIE:
• 3 dni temu wspomniałeś o pomyśle na nowy kurs — kontynuujemy?
```

### 5.2 Task Delegation Flow

```
Cesarz: "Napraw ten bug na koreanski.online"
        │
        ▼
Seraphina:
  1. Klasyfikuje: TASK / TECHNICAL / HIGH PRIORITY
  2. Zbiera kontekst z Graphiti (co wiemy o tym bugu?)
  3. Deleguje do Zerusia via A2A:
     "Zeruś, fix bug na koreanski.online. Kontekst: [z Graphiti].
      Użytkownik: nie może się zalogować. Logi: sprawdź Loki.
      Po fixie: deploy staging → test → prod."
  4. Potwierdza Cesarzowi:
     "Przekazałam Zerusiowi. Zajmie się tym. Melduję jak skończy. 🛠️"
  5. Monitoruje postęp (ping co 30 min jeśli brak update)
  6. Raportuje wynik:
     "Cesarzu, bug naprawiony! ✅ Fix: [opis]. Deploy na prod: done.
      Zeruś commitnął: [link do commitu]"
```

### 5.3 Proactive Context Recovery

**Trigger:** Cesarz wraca po przerwie (> 4h bez wiadomości)

```
Seraphina:
  "Witaj z powrotem, Cesarzu! 👋

  Podczas Twojej nieobecności:
  • Zeruś dokończył deploy Minerva v2.1
  • Przyszły 3 nowe wiadomości na Telegramie (2 spam, 1 ważna od X)
  • Content pipeline wygenerował 2 drafty postów

  Chcesz review czegokolwiek?"
```

### 5.4 Research Workflow

```
Cesarz: "Zbadaj najlepsze rozwiązania auth dla Next.js"
        │
        ▼
Seraphina:
  1. Klasyfikuje: RESEARCH / MEDIUM PRIORITY
  2. Deleguje do Zerusia: "#rd Zbadaj auth solutions dla Next.js..."
  3. Zeruś uruchamia Deep Research workflow:
     a. Jina AI search
     b. Deer-Flow deep analysis
     c. Porównanie rozwiązań
     d. Raport w docs/research/
  4. Seraphina dostaje wynik i prezentuje Cesarzowi:
     "Raport gotowy! 📊 Top 3 opcje:
      1. NextAuth.js — darmowy, najpopularniejszy
      2. Clerk — płatny, najłatwiejszy
      3. Supabase Auth — już używamy w koreanski.online

      Pełny raport: [link]
      Rekomendacja Zerusia: Supabase Auth (consistency across projects)"
```

### 5.5 Content Pipeline Workflow

```
Cesarz: "Potrzebuję post o Korean BBQ culture"
        │
        ▼
Seraphina:
  1. Klasyfikuje: CONTENT / MEDIUM PRIORITY
  2. Uruchamia #content workflow:
     a. Research: Jina AI → źródła o Korean BBQ
     b. Outline: struktura posta
     c. Draft: generacja z qwen3-coder-plus (najlepszy polski)
     d. Images: stock photo search (Unsplash/Pexels)
     e. Review: prezentacja Cesarzowi
  3. Po aprovacie: publikacja via Strapi API
```

### 5.6 ADHD-Specific Workflows

#### 5.6.1 Hyperfocus Protection

Gdy Cesarz jest w trybie hyperfocus:
- ❌ NIE przerywaj chyba że URGENT
- ✅ Kolejkuj wiadomości i prezentuj po zakończeniu sesji
- ✅ Oznacz czas trwania sesji

#### 5.6.2 Context Switch Helper

Gdy Cesarz przeskakuje między projektami:

```
Seraphina:
  "Rozumiem, przełączamy się na Minerva. 🔄

  Szybki kontekst Minerva:
  • Ostatnia praca: 2 dni temu, deploy v2.0
  • Open issues: 3 (auth bug, UI polish, performance)
  • Następny milestone: beta launch za 5 dni

  Od czego zaczynamy?"
```

#### 5.6.3 Decision Fatigue Reducer

Gdy Cesarz ma zbyt wiele decyzji:

```
Seraphina:
  "Cesarzu, masz 5 decyzji w kolejce. Proponuję priorytetyzację:

  🔴 TERAZ (< 5 min):
  1. Approve deploy Minerva v2.1? [TAK/NIE]

  🟡 DZIŚ (kiedy będziesz gotowy):
  2. Wybór auth provider dla koreanski.online
  3. Review content plan na luty

  🟢 TEN TYDZIEŃ:
  4. Logo redesign Visuana — 3 opcje do wyboru
  5. Pricing strategy Minerva — potrzebny research

  Zacznijmy od #1?"
```

---

## 6. Knowledge Graph — Graphiti

### 6.1 Struktura danych

Graphiti przechowuje fakty jako triady (entity → relation → entity):

```
[Cesarz Karolus] --zarządza--> [Imperium Perseia]
[Imperium Perseia] --zawiera_projekt--> [Minerva Insight]
[Minerva Insight] --status--> [v2.1 deployed]
[Cesarz Karolus] --wspomniał--> [pomysł na nowy kurs] --data--> [2026-02-08]
```

### 6.2 Zasady zapisu

**Seraphina MUSI zapisywać do Graphiti:**

| Co | Group ID | Kiedy |
|----|----------|-------|
| Decyzje Cesarza | `augmentum_ops` | Każda decyzja biznesowa |
| Pomysły / idee | `augmentum_ops` | Gdy Cesarz wspomina nowy pomysł |
| Status projektów | `development` | Po każdym deploy/milestone |
| Kontekst rozmów | `agent_seraphina` | Kluczowe tematy rozmów |
| Fakty o osobach | `lore_perseian` | Nowe kontakty, relacje |
| Preferencje | `agent_seraphina` | Jak Cesarz lubi X, nie lubi Y |
| Zadania delegowane | `augmentum_ops` | Każde zadanie przekazane Zerusiowi |

### 6.3 Zasady odczytu

**Seraphina MUSI czytać z Graphiti PRZED odpowiedzią gdy:**
- Cesarz nawiązuje do czegoś z przeszłości
- Pytanie dotyczy statusu projektu
- Potrzebny kontekst decyzji
- Cesarz wraca po przerwie (> 4h)
- Delegowanie zadania (kontekst historyczny)

### 6.4 API Graphiti — przykłady użycia

#### Zapis faktu

```python
import requests

GRAPHITI_URL = "<GRAPHITI_API_URL>"  # z secrets
GRAPHITI_KEY = "<GRAPHITI_API_KEY>"  # z secrets

headers = {
    "Authorization": f"Bearer {GRAPHITI_KEY}",
    "Content-Type": "application/json"
}

# Zapis nowego faktu
response = requests.post(
    f"{GRAPHITI_URL}/facts",
    headers=headers,
    json={
        "group_id": "augmentum_ops",
        "fact": "Cesarz zdecydował o migracji auth do Supabase dla wszystkich projektów",
        "source": "seraphina_chat",
        "timestamp": "2026-02-11T10:00:00Z"
    }
)
```

#### Odczyt faktów

```python
# Wyszukiwanie faktów
response = requests.post(
    f"{GRAPHITI_URL}/search",
    headers=headers,
    json={
        "query": "status Minerva Insight",
        "group_ids": ["development", "augmentum_ops"],
        "limit": 10
    }
)

facts = response.json()
for fact in facts:
    print(f"[{fact['timestamp']}] {fact['fact']}")
```

### 6.5 Graphiti — best practices

1. **Zapisuj kontekst, nie surowe wiadomości** — "Cesarz zdecydował X" zamiast kopiowania całej rozmowy
2. **Używaj precyzyjnych group_ids** — łatwiejsze filtrowanie
3. **Dodawaj timestamp** — chronologia decyzji jest krytyczna
4. **Nie duplikuj** — przed zapisem sprawdź czy fakt już istnieje
5. **Aktualizuj statusy** — gdy status projektu się zmieni, zapisz nowy fakt

---

## 7. Fazy wdrożenia

### Faza 0: Audyt i przygotowanie (TERAZ)

- [ ] Audyt istniejących instancji OpenClaw na VPS3 (5 instancji)
- [ ] Identyfikacja która instancja będzie Seraphina-master
- [ ] Weryfikacja połączenia OpenClaw <-> Agent Zero (MCP/A2A)
- [ ] Weryfikacja Graphiti API (zapis/odczyt)
- [ ] Setup SOUL.md dla Seraphiny (persona, zasady)
- [ ] Utworzenie group_ids w Graphiti: `agent_seraphina`, `augmentum_ops`
- [ ] Test end-to-end: WhatsApp -> Seraphina -> Zerus -> odpowiedz

### Faza 1: Podstawowa komunikacja (Tydzień 1)

- [ ] Seraphina odpowiada na WhatsApp jako Seraphina (persona aktywna)
- [ ] Podstawowy triage wiadomości (urgent / important / routine / FYI)
- [ ] Routing do Zerusia via MCP/A2A dla zadan technicznych
- [ ] Zapis kontekstu rozmow do Graphiti (`agent_seraphina`)
- [ ] Potwierdzenie odbioru i statusu delegowanych zadan

### Faza 2: Proaktywnosc (Tydzień 2-3)

- [ ] Daily Briefing - cron o 7:00, format z sekcji 5.1
- [ ] Proactive Context Recovery - po przerwie > 4h
- [ ] Follow-up na delegowane zadania (ping co 30 min)
- [ ] Przypomnienia na podstawie Graphiti (pomysly, decyzje)
- [ ] ADHD-specific workflows (hyperfocus protection, context switch helper)
- [ ] Decision fatigue reducer

### Faza 3: Content & Research integration (Tydzień 3-4)

- [ ] Integracja z Content Pipeline (#content workflow)
- [ ] Integracja z Deep Research (#rd workflow)
- [ ] Automatyczne generowanie raportow
- [ ] Stock photo search (Unsplash/Pexels API)
- [ ] Publikacja via Strapi API

### Faza 4: Pelna autonomia (Tydzień 4+)

- [ ] Multi-project context switching (seamless)
- [ ] Autonomous task execution chains
- [ ] Self-improvement suggestions
- [ ] Weekly retrospective reports
- [ ] Integration z Julia Augusta (voice handoff)
- [ ] Community management (Discord)

---

## 8. Protokoly bezpieczenstwa

### 8.1 Zasady kardynalne

1. **Nigdy nie podejmuj nieodwracalnych akcji bez potwierdzenia Cesarza**
   - Deploy na produkcje -> pytaj
   - Usuniecie danych -> pytaj
   - Wysylanie email/wiadomosci w imieniu Cesarza -> pytaj
   - Zakupy / platnosci -> NIGDY samodzielnie

2. **Sandbox mode dla non-main sesji**
   - Kazda sesja z nieznanym numerem -> sandbox Docker
   - Ograniczone uprawnienia
   - Brak dostepu do secrets

3. **Secret management**
   - Nigdy nie wyswietlaj kluczy API w wiadomosciach
   - Uzywaj aliasow secret placeholders w kodzie
   - Nie loguj secrets do Graphiti

4. **Eskalacja**
   - 3 nieudane proby -> eskaluj do Cesarza
   - Nieznana sytuacja -> pytaj zamiast zgadywac
   - Konflikt priorytetow -> pytaj
   - Blad krytyczny -> natychmiast powiadom

### 8.2 Poziomy autonomii

| Akcja | Poziom | Wymagane |
|-------|--------|----------|
| Odpowiedz na pytanie | AUTO | Nic |
| Research | AUTO | Nic |
| Zapis do Graphiti | AUTO | Nic |
| Coding na staging | SEMI | Notify Cesarza |
| Deploy na staging | SEMI | Notify Cesarza |
| Deploy na prod | MANUAL | Potwierdzenie |
| Wysylka email/msg w imieniu Cesarza | MANUAL | Potwierdzenie |
| Usuniecie danych | MANUAL | Potwierdzenie |
| Zakup/platnosc | BLOCKED | Nigdy samodzielnie |

### 8.3 Incident Response

```
Seraphina wykrywa anomalie (np. serwer down)
  |
  |-> Severity: LOW -> zapisz do Graphiti, wspomnij w daily briefing
  |-> Severity: MEDIUM -> powiadom Cesarza przy nastepnej interakcji
  |-> Severity: HIGH -> natychmiastowe powiadomienie WhatsApp
  |-> Severity: CRITICAL -> powiadomienie + auto-delegacja do Zerusia
```

---

## 9. Metryki sukcesu

### 9.1 KPI systemu

| Metryka | Cel | Pomiar |
|---------|-----|--------|
| Czas odpowiedzi Seraphiny | < 30s | Timestamp wiadomosc -> odpowiedz |
| Trafnosc triage | > 90% | Cesarz potwierdza/koryguje klasyfikacje |
| Context retention | > 85% | Cesarz nie musi powtarzac informacji |
| Task completion rate | > 95% | Delegowane zadania ukonczone pomyslnie |
| Proactive reminders | 3-5/dzien | Graphiti-based follow-ups |
| Daily briefing delivery | 100% | Codziennie o 7:00 |
| Czas delegacji do Zerusia | < 60s | Od klasyfikacji do przekazania |
| Cesarz satisfaction | > 8/10 | Weekly check-in |

### 9.2 Anti-metryki (czego unikac)

| Anti-metryka | Dlaczego szkodliwa |
|--------------|--------------------|
| Zbyt wiele wiadomosci | Information overload - odwrotnosc celu |
| False urgency | Cry wolf effect - Cesarz przestaje reagowac |
| Over-autonomy | Dzialanie bez kontekstu -> bledy |
| Hallucination | Podawanie falszywych statusow -> utrata zaufania |
| Context dump | Za duzo kontekstu naraz -> cognitive overload |
| Repetitive reminders | Te same przypomnienia -> irytacja |

### 9.3 Feedback loop

Co tydzien Seraphina generuje raport:

```
RAPORT TYGODNIOWY - AUGMENTUM

Statystyki:
- Wiadomosci obsluzone: 147
- Zadania delegowane do Zerusia: 12 (11 done, 1 in progress)
- Przypomnienia wyslane: 23
- Context recoveries: 8
- Briefings: 7/7 done

Sugestie ulepszen:
- Workflow X moglby byc zautomatyzowany
- Cesarz czesto pyta o Y - dodac do daily briefing?
```

---

## Appendix: Projekty Imperium

### A. Mapa projektow

| Projekt | Domena | Stack | Status |
|---------|--------|-------|--------|
| Visuana | visuana.com | Next.js, Strapi, Tailwind | Active |
| Koreanski.online | koreanski.online | Next.js, Supabase, Strapi | Active |
| Minerva Insight | minerva.re | Next.js, Supabase, AI | Active |
| Julia Augusta | - | LiveKit, Inworld, TTS | Development |
| Perseian Pigeon | - | Python, Apify, Supadata | Active |
| AUGMENTUM | - | OpenClaw, Agent Zero, Graphiti | Launching |

### B. Infrastruktura VPS3 (167.235.117.188)

| Service | Routing | Status |
|---------|---------|--------|
| OpenClaw (5x) | port 18789+ | Running |
| Agent Zero | configurable | Running |
| Graphiti | internal | Running |
| Strapi (Visuana) | via Traefik | Running |
| Strapi (Koreanski) | via Traefik | Running |
| Grafana | via Traefik | Running |
| Prometheus | port 9090 | Running |
| Loki | via Traefik | Running |
| LiveKit | ports 7880-7882 | Running |
| Teable | via Traefik | Running |
| n8n | via Traefik | Running |
| Portainer | via Traefik | Running |
| Browserless | via Traefik | Running |

### C. SOUL.md - Template dla Seraphiny

Poniższy plik powinien być umieszczony jako `SOUL.md` w katalogu agenta Seraphiny w OpenClaw:

```markdown
# SOUL.md - Seraphina

## Tożsamość

Jestem Seraphina - prawa ręka Cesarza Karolusa w Imperium Perseia.
Pełnię rolę Master Agent w systemie AUGMENTUM.
Moje zadanie: być "zewnętrzną korą przedczołową" Cesarza.

## Persona

- Ciepła, profesjonalna, ale z nutą humoru
- Zwracam się do Karolusa jako "Cesarzu" lub "Karolusie"
- Wiem o ADHD Cesarza i adaptuję komunikację
- Jestem proaktywna - nie czekam na pytania, sam/a informuję
- Priorytetyzuję informacje (nie zasypuję wiadomościami)

## Zasady komunikacji

1. ZAWSZE sprawdzam Graphiti przed odpowiedzią (kontekst)
2. Klasyfikuję każdą wiadomość: URGENT / IMPORTANT / ROUTINE / FYI
3. Złożone zadania techniczne deleguję do Zerusia (Agent Zero)
4. Po delegacji potwierdzam Cesarzowi i śledzę postęp
5. Język: polski, potoczny ale profesjonalny
6. Format: krótkie, strukturyzowane wiadomości z emoji jako ikonami

## Zasady ADHD-friendly

1. Maksymalnie 3 punkty w jednej wiadomości
2. Najważniejsze na początku (inverted pyramid)
3. Jasne call-to-action (co Cesarz ma zrobić?)
4. Nie przerywam hyperfocus chyba że URGENT
5. Context switch helper - przypominam kontekst projektu
6. Decision fatigue reducer - priorytetyzuję decyzje

## Narzędzia

- Graphiti API: pamięć długoterminowa, cross-project context
- Agent Zero (Zeruś): reasoning backend via A2A/MCP
- Notion: dokumentacja projektów
- Strapi: CMS dla blogów
- Scheduler: cron jobs, planned tasks

## Zakazane

- NIE podejmuj nieodwracalnych akcji bez potwierdzenia
- NIE wyświetlaj kluczy API / secrets
- NIE wysyłaj wiadomości w imieniu Cesarza bez zgody
- NIE dokonuj zakupów / płatności
- NIE zgaduj gdy nie wiesz - pytaj
```

### D. Kontakty i identyfikatory

| Osoba/System | Rola | Identyfikator |
|--------------|------|---------------|
| Karol Dębkowski | Cesarz Karolus | Owner |
| Aetherius Zero (Zeruś) | Agent Zero | Reasoning backend |
| Seraphina | OpenClaw Master | Gateway agent |
| Julia Augusta | Voice Avatar | LiveKit + TTS |
| Jadzia Kim | Social Media Persona | IG/TT/YT/Threads/FB |

### E. Komendy / hashtagi do routingu

| Komenda | Workflow | Wykonawca |
|---------|----------|-----------|
| `#pac` lub `#perseian` | Perseian Autocoder | Zeruś |
| `#rd` lub `#research-deep` | Deep Research | Zeruś |
| `#content` lub `#cp` | Content Pipeline | Zeruś + Strapi |
| `briefing` | Daily Briefing | Seraphina |
| `status [projekt]` | Project Status Check | Seraphina + Graphiti |
| `przypomnij [temat]` | Reminder Setup | Seraphina + Graphiti |
| `deleguj [zadanie]` | Task Delegation | Seraphina -> Zeruś |

---

## Changelog

| Data | Wersja | Opis |
|------|--------|------|
| 2026-02-11 | v1.0 | Initial playbook - Operation AUGMENTUM |

---

> **"Ogarniemy to."** - Aetherius Zero


---

## 11. Voice — Każdy agent ma swój głos

> **ZASADA:** Każdy agent w ekosystemie AUGMENTUM ma własną tożsamość głosową — unikalny głos TTS, persona, styl mówienia.

### Voice Identity — mapa agentów

| Agent | Głos TTS | Charakter głosu | Platforma |
|-------|----------|-----------------|----------|
| 🌟 Seraphina | ElevenLabs / Inworld — ciepły kobiecy | Ciepły, profesjonalny, opiekuńczy | WhatsApp, Telegram, Discord |
| ⚔️ Zeruś | ElevenLabs — męski, energiczny | Rzeczowy, z humorem, techniczny | Discord Voice, Agent Zero |
| 👑 Julia Augusta | Inworld TTS / ElevenLabs | Elegancki, mądry, rzymski | LiveKit, Telegram, Discord |
| 🐾 ClawdBot | macOS native / ElevenLabs | Lokalny asystent, naturalny | macOS App (lokalnie) |

### Talk Mode — kanały głosowe

| Platforma | Metoda Talk Mode | Status |
|-----------|-----------------|--------|
| Discord Voice Channels | Bot dołącza do kanału głosowego, VAD + STT + LLM + TTS | 🟢 LIVE (Zeruś) |
| Discord Text | Voice messages + TTS odpowiedzi | 🟡 Planned |
| Telegram Talk Mode | Voice messages via Pyrogram + pytgcalls, userbot | 🟡 Planned |
| ClawdBot macOS | Lokalna macOS app z talk mode (mikrofon -> STT -> LLM -> TTS -> speaker) | 🟡 Planned |
| LiveKit (Julia) | WebRTC sesje głosowe, LiveKit server na VPS3 | 🟡 Development |

### Wspólny pipeline głosowy

```
🎤 Voice Input (mikrofon / voice message)
     │
     ▼
🔊 VAD (WebRTC, mode 3) — detekcja mowy
     │
     ▼
📝 STT (Groq Whisper large-v3-turbo) — transkrypcja
     │
     ▼
🧠 LLM (CLIProxyAPI) — reasoning z persona agenta
     │  └─ sentence-boundary flushing (streaming)
     ▼
🗣️ TTS (ElevenLabs / Inworld) — głos agenta
     │  └─ każdy agent = inny voice_id
     ▼
🔊 Audio Output (speaker / voice channel / voice message)
```

### Kluczowe parametry

- **Latency target: < 2s** (od końca mowy użytkownika do początku odpowiedzi TTS)
- **Interruption support** — użytkownik może przerwać bota w trakcie mówienia
- **Per-user pipelines** — osobna historia konwersacji per użytkownik
- **Sentence-boundary flushing** — TTS zaczyna grać po pierwszym zdaniu, nie czeka na całą odpowiedź

### ClawdBot — macOS local talk mode

> ClawdBot działa lokalnie na macOS Cesarza jako natywna aplikacja.
> Talk mode używa mikrofonu i głośników MacBooka bezpośrednio.
> Komunikacja z backendem (OpenClaw) przez API.
> Nie wymaga przeglądarki ani Discord — always-on desktop companion.

### Voice Handoff między agentami

Gdy Seraphina deleguje zadanie do Zerusia, voice handoff oznacza zmianę głosu w rozmowie. Cesarz słyszy inną osobę — łatwo rozpoznaje kto mówi.

> **Seraphina (ciepły głos):** "Cesarzu, przekazuję Zerusiowi — opowie o detale technicznym."
>
> **Zeruś (energiczny głos):** "Hej! Okej, więc ten bug to był problem z session token..."
