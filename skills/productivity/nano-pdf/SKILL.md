---
name: nano-pdf
description: "Edit text in existing PDFs via natural-language prompts."
version: 1.0.0
author: community
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [PDF, Documents, Editing, NLP, Productivity]
    homepage: https://pypi.org/project/nano-pdf/
    related_skills: [pdf, ocr-and-documents]
---

> **IMOLED-Anpassung (2026-08-20):** Dieser Skill stammt aus dem Studien-Fork `NousResearch/hermes-agent` und läuft hier unter Claude Code, nicht unter der Hermes-Laufzeit. Übersetzung: Der Skill-Ordner `~/.hermes/skills/nano-pdf/` heißt hier `~/Github/forks/NousResearch--hermes-agent/skills/productivity/nano-pdf/` (Symlink: `#COWORK/IMOLED-digital/skills/nano-pdf/`). Zustands-Pfade `~/.hermes/...` heißen hier `~/.config/imoled/hermes-skills/nano-pdf/...` (bei Bedarf anlegen). Werkzeug-Übersetzung: `web_search`/`web_extract` = WebSearch/WebFetch, `browser_navigate` = Browser-Werkzeuge, Terminal-Tool = Bash. `create_job(...)` und `hermes cron` gibt es hier NICHT: keine neuen Scheduled Tasks (Andreas-Setzung 28.05.2026); wiederkehrende Ticks laufen über /loop in der Session oder als Vorschlag an Andreas.

# nano-pdf

Edit PDFs using natural-language instructions. Point it at a page and describe what to change. For structural PDF work (merge, split, forms, watermarks, creation), see the `pdf` skill; for text extraction from scans, see `ocr-and-documents`.

## Prerequisites

```bash
# Install with uv (recommended — already available in Hermes)
uv pip install nano-pdf

# Or with pip
pip install nano-pdf
```

## Usage

```bash
nano-pdf edit <file.pdf> <page_number> "<instruction>"
```

## Examples

```bash
# Change a title on page 1
nano-pdf edit deck.pdf 1 "Change the title to 'Q3 Results' and fix the typo in the subtitle"

# Update a date on a specific page
nano-pdf edit report.pdf 3 "Update the date from January to February 2026"

# Fix content
nano-pdf edit contract.pdf 2 "Change the client name from 'Acme Corp' to 'Acme Industries'"
```

## Notes

- Page numbers may be 0-based or 1-based depending on version — if the edit hits the wrong page, retry with ±1
- Always verify the output PDF after editing (use `read_file` to check file size, or open it)
- The tool uses an LLM under the hood — requires an API key (check `nano-pdf --help` for config)
- Works well for text changes; complex layout modifications may need a different approach
