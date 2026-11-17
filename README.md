# 1even Platform: documents

Documents from 1even.lab about 1even Platform, a self-hosted platform that runs an AI
agent on top of a company's data stack. The agent answers questions about data,
investigates pipeline failures and prepares changes within the user's permissions.

Each document comes in two forms, a PDF for a person and Markdown for an AI agent, and in
two languages, English and Russian.

[Русская версия этого описания](#по-русски) ниже.

## Who reads what

| Reader | Open | Format |
|---|---|---|
| A person | [Platform overview, EN](for-people/1even-platform-overview.en.pdf) · [RU](for-people/1even-platform-overview.pdf) | PDF, 12 pages |
| An AI agent | [`AGENTS.md`](AGENTS.md), then [`overview.en.md`](for-agents/overview.en.md) or [`overview.md`](for-agents/overview.md) (RU) | Markdown |

If you hand this repository to an agent (Claude Code, Codex, Cursor), point it at
`AGENTS.md`. The agent does not need the PDFs: the same text is in `for-agents/`.

## What the overview covers

- why the platform matters to teams that already use AI agents;
- what the agent does for analysts, data engineers, developers, finance and security;
- six scenarios: data questions, incidents, reports, changes, team memory, configuration
  without a developer;
- the access model and what goes into the audit log;
- two diagrams: how a request travels and how memory works;
- how to start a pilot and what the current version cannot do.

## Layout

| Folder | Contents |
|---|---|
| [`for-people/`](for-people/) | The overview as PDF: `…overview.en.pdf` (English), `…overview.pdf` (Russian) |
| [`for-agents/`](for-agents/) | The same overview as Markdown, with a text description of the diagrams: `overview.en.md`, `overview.md` |
| [`diagrams/`](diagrams/) | SVG diagrams. English: [request path](diagrams/request-path.en.svg), [memory](diagrams/memory.en.svg). Russian: [путь запроса](diagrams/request-path.svg), [память](diagrams/memory.svg) |

Files without a language suffix are Russian; `.en` marks the English edition. Both
editions carry the same content and describe platform version 0.21.6.

The CAPTURE Framework, the method 1even.lab uses to introduce agentic analytics, lives in
its own repository, `1even-lab/capture-framework`.

## Licence

The text and diagrams in this repository are licensed under Creative Commons
Attribution-ShareAlike 4.0 International (CC BY-SA 4.0); the full text is in
[`LICENSE`](LICENSE). You may use, share and adapt them, including commercially, as long
as you credit the source and distribute adaptations under the same licence.

Suggested attribution: 1even Platform documentation by Max Ivanov, 1even.lab
(github.com/1even-lab/docs), CC BY-SA 4.0.

The platform's code is distributed separately under the MIT licence.

---

## По-русски

Документы лаборатории 1even.lab о платформе 1even Platform. Это self-hosted платформа,
на которой ИИ-агент работает поверх дата-стека компании: отвечает на вопросы по данным,
разбирает сбои пайплайнов и готовит изменения в пределах прав пользователя.

Каждый документ есть в двух видах (PDF для человека, Markdown для ИИ-агента) и на двух
языках.

| Кто читает | Что открыть |
|---|---|
| Человек | [Обзор платформы, RU](for-people/1even-platform-overview.pdf) · [EN](for-people/1even-platform-overview.en.pdf) |
| ИИ-агент | [`AGENTS.md`](AGENTS.md), затем [`overview.md`](for-agents/overview.md) или [`overview.en.md`](for-agents/overview.en.md) |

Файлы без языкового суффикса русские, суффикс `.en` означает английскую версию. Схемы
лежат в [`diagrams/`](diagrams/). Фреймворк CAPTURE находится в отдельном репозитории
`1even-lab/capture-framework`.

Тексты и схемы распространяются по лицензии CC BY-SA 4.0, полный текст в файле
[`LICENSE`](LICENSE). Указание авторства: 1even Platform documentation by Max Ivanov,
1even.lab (github.com/1even-lab/docs), CC BY-SA 4.0. Код платформы распространяется
отдельно, под лицензией MIT.
