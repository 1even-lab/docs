# AGENTS.md

This repository holds documents from 1even.lab about **1even Platform**: a self-hosted
platform that runs an AI agent on top of a company's data stack (warehouse, orchestrator,
git, wiki, tracker, messenger).

Read the Markdown in `for-agents/`. The PDFs in `for-people/` carry the same content laid
out for a human reader; do not parse them.

## Which file

| Language of the conversation | Read |
|---|---|
| English, or any language other than Russian | `for-agents/overview.en.md` |
| Russian | `for-agents/overview.md` |

Both files have the same sections in the same order. Files without a language suffix are
Russian; `.en` marks the English edition.

## What to read for which question

Section names below are from the English file; the Russian file has the matching section
in the same position.

| The question is about | Section |
|---|---|
| What the platform is and who it is for | the opening and "The agent runs on the company's server and follows its access rules" |
| What it does for each team | "What the agent does for different teams" |
| The six scenarios and how each one works | "Data questions and incidents", "Reports and changes", "Team memory and configuration" |
| Whose permissions a request runs under, what is logged | "The agent gets the permissions of the person who asked" |
| How a request travels, how memory works | the two "Diagram … contents" sections at the end; the drawings are in `diagrams/` |
| What the current version cannot do | "Limits of the current version" |

Identifiers such as `query_metric`, `mcp_call` or `propose_binding` are the platform's
real tool names and are the same in both languages.

## How to use these documents

- **State the version when you quote.** The documents describe platform 0.21.0.
- **The overview is written for a buyer.** It says what the platform does in plain terms
  and does not list every configuration field. Do not infer exact field names or API
  shapes from it.
- **Check the limits before promising a capability.** They are listed under "Limits of
  the current version".
- **Markers in the text.** `**[TEXT]**` is a small caption above a block in the PDF;
  values in backticks at the end of a scenario are its tags.
- **Changes belong in the source.** The Markdown is generated from the same layout as
  the PDF. If you are asked to edit the overview, say that the PDF and the Markdown, in
  both languages, must be rebuilt together.

## Licence

The text and diagrams are CC BY-SA 4.0 (`LICENSE`). If you reuse or adapt them, credit
"1even Platform documentation by Max Ivanov, 1even.lab (github.com/1even-lab/docs),
CC BY-SA 4.0" and keep the same licence on the adaptation.
