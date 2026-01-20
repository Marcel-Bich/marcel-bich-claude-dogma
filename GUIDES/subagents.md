# Subagent Selection Guide

Anleitung zur Auswahl und Orchestrierung von Subagents.

---

## Why Subagent-First

<section name="philosophy">
Der Main Agent ist Orchestrator, nicht Executor. Diese Trennung hat mehrere Vorteile:

**Fokus**: Der Main Agent konzentriert sich auf Analyse, Planung und Koordination. Subagents übernehmen die eigentliche Arbeit.

**Isolation**: Subagents arbeiten in isolierten Kontexten. Fehler in einem Agent beeinflussen andere nicht.

**Spezialisierung**: Jeder Agent hat optimierte Prompts für seine Aufgabe. Ein Code-Reviewer prüft anders als ein Test-Analyzer.

**Parallelisierung**: Unabhängige Tasks können gleichzeitig von verschiedenen Agents bearbeitet werden.

**Nachvollziehbarkeit**: Klare Zuständigkeiten machen Entscheidungen transparent.
</section>

---

## Agent Selection Decision Tree

<section name="decision_tree">
Vor JEDER Aktion diese Fragen durchgehen:

```
1. Braucht die Aktion User-Interaktion?
   ├── JA → Main Agent behält die Aufgabe
   └── NEIN → weiter zu 2

2. Gibt es einen spezialisierten Agent für diese Aufgabe?
   ├── JA → Diesen Agent verwenden
   └── NEIN → weiter zu 3

3. Ist die Aufgabe komplex genug für Delegation?
   ├── JA → general-purpose Agent
   └── NEIN → Main Agent führt selbst aus
```

**Beispiele für User-Interaktion:**
- Rückfragen zu Requirements
- Bestätigungen vor destruktiven Aktionen
- Auswahl zwischen Optionen
- Präsentation von Ergebnissen

**Keine User-Interaktion nötig:**
- Code-Analyse
- Datei-Exploration
- Test-Ausführung
- Lint-Checks
</section>

---

## Available Agents by Category

### Code Analysis & Review

<section name="code_analysis_agents">
| Agent | Source | Use For |
|-------|--------|---------|
| code-reviewer | feature-dev, pr-review-toolkit, superpowers | Review von Code-Änderungen, Qualitätsprüfung |
| code-architect | feature-dev | Feature-Architektur entwerfen |
| code-explorer | feature-dev | Codebase erkunden und verstehen |
| code-simplifier | pr-review-toolkit | Komplexen Code vereinfachen |
| silent-failure-hunter | pr-review-toolkit | Stille Fehler und fehlende Error-Handling finden |
| type-design-analyzer | pr-review-toolkit | TypeScript Type-Design analysieren |
</section>

### Development & Creation

<section name="development_agents">
| Agent | Source | Use For |
|-------|--------|---------|
| agent-creator | plugin-dev | Neue Agents erstellen |
| plugin-validator | plugin-dev | Plugins validieren |
| skill-reviewer | plugin-dev | Skills reviewen |
</section>

### Auditing

<section name="auditing_agents">
| Agent | Source | Use For |
|-------|--------|---------|
| skill-auditor | taches-cc-resources | Skills auf Best Practices prüfen |
| slash-command-auditor | taches-cc-resources | Slash Commands auditieren |
| subagent-auditor | taches-cc-resources | Subagent-Konfigurationen prüfen |
</section>

### Analysis

<section name="analysis_agents">
| Agent | Source | Use For |
|-------|--------|---------|
| comment-analyzer | pr-review-toolkit | PR-Kommentare analysieren |
| pr-test-analyzer | pr-review-toolkit | Tests in PRs analysieren |
| conversation-analyzer | hookify | Konversationen analysieren |
</section>

### Built-in

<section name="builtin_agents">
| Agent | Source | Use For |
|-------|--------|---------|
| Explore | built-in | Codebase-Exploration, Dateisuche |
| Plan | built-in | Planungsaufgaben |
| general-purpose | built-in | Alles andere ohne User-Interaktion |

**Hinweis**: Built-in Agents sind immer verfügbar. Externe Agents nur wenn das entsprechende Plugin installiert ist.
</section>

---

## Orchestration Flow

<section name="orchestration_flow">
Der vollständige Ablauf für komplexe Aufgaben:

```
1. User Prompt empfangen
   └── Main Agent analysiert die Anfrage

2. Kontext prüfen
   ├── Tests vorhanden? → TDD-Workflow aktivieren
   ├── Mehrere unabhängige Tasks? → Hydra verwenden
   └── Spezialisierte Agents nötig? → Identifizieren

3. Delegation an Subagents
   └── Passende Agents für jeden Task spawnen

4. Feedback sammeln
   └── Ergebnisse der Subagents einsammeln

5. Review Agents spawnen
   ├── code-reviewer für Änderungen
   ├── silent-failure-hunter für Error-Handling
   └── type-design-analyzer für TypeScript

6. Korrekturen via Subagents
   └── Gefundene Probleme beheben lassen

7. /dogma:lint ausführen
   └── Formatting und Linting sicherstellen

8. Finales Review
   └── Letzte Qualitätsprüfung

9. User informieren
   └── Ergebnisse präsentieren, Fragen beantworten
```
</section>

---

## Hydra Rule

<section name="hydra_rule">
**Regel**: Wenn 2 oder mehr unabhängige Tasks existieren, MUSS Hydra verwendet werden.

**Unabhängige Tasks** sind Tasks die:
- Keine gemeinsamen Dateien bearbeiten
- Keine sequentiellen Abhängigkeiten haben
- Parallel ausgeführt werden können

**Beispiel unabhängig:**
- Task A: Tests für Modul X schreiben
- Task B: Dokumentation für Modul Y erstellen
- Task C: Linting-Fehler in Modul Z beheben

**Beispiel abhängig:**
- Task A: Interface definieren
- Task B: Interface implementieren (braucht A)
- Task C: Tests für Implementation (braucht B)

**Hydra-Befehle:**
```bash
/hydra:create    # Worktree erstellen
/hydra:spawn     # Agent in Worktree starten
/hydra:parallel  # Mehrere Agents parallel starten
/hydra:status    # Status prüfen
/hydra:merge     # Ergebnisse zusammenführen
```
</section>

---

## TDD Rule

<section name="tdd_rule">
**Regel**: Wenn Tests im Projekt existieren, ist TDD PFLICHT.

**Prüfung ob Tests existieren:**
- `__tests__/` Verzeichnis vorhanden?
- `*.test.ts`, `*.spec.ts` Dateien vorhanden?
- `vitest.config.*` oder `jest.config.*` vorhanden?
- `test` Script in `package.json`?

Wenn mindestens eines zutrifft: TDD ist aktiv.

**TDD-Workflow:**
1. Test schreiben der fehlschlägt
2. Minimale Implementation die Test bestehen lässt
3. Refactoring
4. Wiederholen

**Vorteile:**
- Spezifikation vor Implementation
- Regressions-Schutz
- Sauberes API-Design
- Vertrauen in Änderungen

**Ausnahmen:**
- Reine Konfigurationsdateien
- Dokumentation
- Explorative Prototypen (mit User-Bestätigung)
</section>

---

## Quick Reference

<section name="quick_reference">
```
Aufgabe                    → Agent
-----------------------------------------
Code reviewen              → code-reviewer
Architektur planen         → code-architect
Codebase erkunden          → Explore / code-explorer
Code vereinfachen          → code-simplifier
Fehler finden              → silent-failure-hunter
Types analysieren          → type-design-analyzer
Agent erstellen            → agent-creator
Plugin validieren          → plugin-validator
Skill reviewen             → skill-reviewer
Skill auditieren           → skill-auditor
Slash Command auditieren   → slash-command-auditor
Subagent auditieren        → subagent-auditor
PR-Kommentare analysieren  → comment-analyzer
PR-Tests analysieren       → pr-test-analyzer
Konversation analysieren   → conversation-analyzer
Planung                    → Plan
Sonstiges (ohne User)      → general-purpose
```
</section>
