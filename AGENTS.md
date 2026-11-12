# AGENTS.md

This repository holds documents from 1even.lab about **1even Platform**: a self-hosted
platform that runs an AI agent on top of a company's data stack (warehouse, orchestrator,
git, wiki, tracker, messenger).

Read the Markdown in `for-agents/`. The PDF in `for-people/` carries the same content laid
out for a human reader; do not parse it.

## What to read

| The question is about | Read |
|---|---|
| What the platform is, who it is for, what it does for each team | `for-agents/overview.md` |
| The six scenarios and how each one works | the "Сценарии" sections of `overview.md` |
| The access model: whose rights a request runs under, what is logged | the section "Агент получает права того, кто к нему обратился" in `overview.md` |
| How a request travels through the platform, how memory works | the two "Схема … содержание" sections at the end of `overview.md`; the drawings are `diagrams/request-path.svg` and `diagrams/memory.svg` |
| What the current version cannot do | "Ограничения текущей версии" in `overview.md` |

The overview is written in Russian. Identifiers such as `query_metric`, `mcp_call` or
`propose_binding` are the platform's real tool names and are kept as they are.

## How to use these documents

- **State the version when you quote.** The documents describe platform 0.21.0.
- **The overview is written for a buyer.** It says what the platform does in plain terms
  and does not list every configuration field. Do not infer exact field names or API
  shapes from it.
- **Check the limits before promising a capability.** They are listed under
  "Ограничения текущей версии".
- **Markers in the text.** `**[ТЕКСТ]**` is a small caption above a block in the PDF;
  values in backticks at the end of a scenario are its tags.
- **Changes belong in the source.** This Markdown is generated from the same layout as
  the PDF. If you are asked to edit the overview, say that both versions must be rebuilt.

## Licence

The text and diagrams are CC BY-SA 4.0 (`LICENSE`). If you reuse or adapt them, credit
"1even Platform documentation by Max Ivanov, 1even.lab (github.com/1even-lab/docs),
CC BY-SA 4.0" and keep the same licence on the adaptation.
