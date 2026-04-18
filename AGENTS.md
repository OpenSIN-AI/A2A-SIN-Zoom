# A2A-SIN-Zoom — AGENTS.md

## Purpose

Autonomous Zoom meeting and chat integration agent operating within the Team Messaging ecosystem.

## Rules

- NEVER ask user for manual help — find your own way
- ALWAYS use opencode CLI for LLM calls — never direct API calls
- ALWAYS log errors to the approved artifact storage surface — never leave logs locally
- ALWAYS follow the Google account matrix for any Google operations
- ALWAYS use the approved OpenSIN browser automation surfaces — never raw nodriver

## LLM Call Architecture

```python
import subprocess, json

def call_llm(prompt, timeout=120):
    result = subprocess.run(
        ["opencode", "run", prompt, "--format", "json"],
        capture_output=True, text=True, timeout=timeout,
    )
    parts = []
    for line in result.stdout.splitlines():
        try:
            ev = json.loads(line)
            if ev.get("type") == "text":
                parts.append(ev.get("part", {}).get("text", ""))
        except json.JSONDecodeError:
            pass
    return "".join(parts).strip()
```

**Model:** `opencode/qwen3.6-plus-free` + `--fallback opencode/minimax-m2.5-free`

## PARALLEL-EXPLORATION MANDATE (PRIORITY -4.5)

Bei grossen Codebases (100k+ Zeilen, 1000+ Dateien) MUESSEN Agenten **5-10 parallele explore + 5-10 librarian-Agenten** starten.

```
task(subagent_type="explore", run_in_background=true, load_skills=[], description="Find APIs", prompt="[CONTEXT]: Grosse Codebase. [GOAL]: Alle API-Endpunkte. [REQUEST]: Dateipfade + Beschreibung.")
task(subagent_type="explore", run_in_background=true, load_skills=[], description="Find Services", prompt="[CONTEXT]: Grosse Codebase. [GOAL]: Alle Services. [REQUEST]: Dateipfade + Methoden.")
task(subagent_type="librarian", run_in_background=true, load_skills=[], description="Framework Docs", prompt="[GOAL]: Offizielle Doku. [REQUEST]: Best Practices.")
```

**HARTE REGELN:**
1. `run_in_background=true` ist PFLICHT
2. `load_skills=[]` ist PFLICHT
3. WARTEN bis ALLE background-Agenten fertig sind
4. Ergebnisse deduplizieren und zusammenfuehren

## Subagenten-Modelle

| Subagent | Modell | Fallback-Kette |
|:---|:---|:---|
| **explore** | `nvidia-nim/stepfun-ai/step-3.5-flash` | gemini-3-flash → gpt-5.4 → gemini-3.1-pro → claude-sonnet → qwen |
| **librarian** | `nvidia-nim/stepfun-ai/step-3.5-flash` | gemini-3-flash → gpt-5.4 → gemini-3.1-pro → claude-sonnet → qwen |

## Agent Config System v5

- **Team:** Team Messaging
- **Manager:** A2A-SIN-Messaging
- **Config:** `my-sin-team-messaging.json`
- **Team Register:** `oh-my-sin.json`

→ [Full Documentation](https://github.com/OpenSIN-AI/OpenSIN-documentation/blob/main/docs/guide/agent-configuration.md)

## Boundary Guidance

When modifying this repo:

- Prefer Zoom meeting, chat, and session-support work.
- Do not turn this repo into a generic messaging bucket.
- Do not redefine organization docs, architecture, runtime canon, or non-Zoom ownership here.
- Move non-Zoom behavior back to the repos that own those surfaces.

## License

Apache-2.0
