# Project Memory für Claude Code

## Imports
@.claude/conventions/typescript.md
@.claude/conventions/git.md
@.claude/commands.md
@.claude/architecture.md
@.claude/project-context.md

## Quick Reference
Dies ist die zentrale CLAUDE.md Datei. Alle projektspezifischen Informationen sind modular in Unterdateien organisiert.

## Todo Management System
Dieses Projekt nutzt ein Git-basiertes Todo-System mit `todos.json`.

### Todo-Befehle für Claude
- **Neues Todo**: "Erstelle ein neues Todo: [Beschreibung]"
- **Todo erledigen**: "Markiere Todo [ID oder Titel] als erledigt"
- **Todo löschen**: "Lösche Todo [ID oder Titel]"
- **Todos anzeigen**: "Zeige alle offenen Todos"
- **Todo aktualisieren**: "Ändere Priorität von Todo [ID] auf high/medium/low"

### Todo Viewer
Öffne `todo-viewer.html` im Browser um:
- Alle Todos zu sehen und zu filtern
- Titel inline zu editieren
- Claude-Befehle zu generieren für Änderungen

### Todo-Struktur
Todos haben folgende Felder:
- `id`: Eindeutige ID (UUID)
- `title`: Kurzer Titel
- `description`: Ausführliche Beschreibung
- `status`: pending | in-progress | done
- `priority`: high | medium | low
- `tags`: Array von Tags für Kategorisierung

