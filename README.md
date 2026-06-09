# ai-skills

Beispiel-Repository mit wiederverwendbaren GitHub Copilot Skills.

## Skill-Übersicht

Die Skills liegen unter `.github/skills/<skill-name>/SKILL.md`.

| Skill | Beschreibung |
| --- | --- |
| `compliance-code-audit-reviewer` | Führt Compliance-orientierte Code-Audits durch (DORA, VAIT, NIS2, GDPR/DSGVO) und liefert priorisierte Findings, Control-Mapping und Maßnahmen. |
| `github-issue-implementer` | Orchestriert die Umsetzung eines GitHub Issues: Anforderungen verstehen, Implementierung delegieren, Validierung delegieren und Ergebnis zusammenfassen. |
| `github-issue-implementation-executor` | Subagent für die eigentliche, minimal-invasive Code-Implementierung inkl. passender Tests auf Basis definierter Issue-Anforderungen. |
| `github-issue-validation-runner` | Subagent für die Validierung der Änderungen mit priorisierten Checks und nachvollziehbarer Ergebnis-/Risiko-Dokumentation. |

## Skills installieren

1. Gewünschten Skill-Ordner in dein Repository unter `.github/skills/<skill-name>/` kopieren.
2. Sicherstellen, dass die Datei `SKILL.md` im Zielordner liegt.
3. Änderungen committen und ins Repository pushen.
4. Copilot im Repository neu laden (z. B. neue Chat-Session starten), damit der Skill erkannt wird.

## Skills nutzen

1. In Copilot Chat den Skill über Namen und Kontext ansprechen (z. B. Aufgabe + gewünschter Skill).
2. Benötigte Eingaben mitgeben (z. B. Scope, Issue-URL, Akzeptanzkriterien, Constraints).
3. Rückfragen des Skills beantworten, falls Pflichtinformationen fehlen.
4. Ergebnis prüfen und ggf. Folgeaktionen (Implementierung, Validierung, Review) ausführen.
