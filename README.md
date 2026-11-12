# 1even Platform: документы

Документы лаборатории 1even.lab о платформе 1even Platform. Это self-hosted платформа,
на которой ИИ-агент работает поверх дата-стека компании: отвечает на вопросы по данным,
разбирает сбои пайплайнов и готовит изменения в пределах прав пользователя.

Каждый документ есть в двух видах: PDF для человека и Markdown для ИИ-агента.

## Кому что читать

| Кто читает | Что открыть | Формат |
|---|---|---|
| Человек | [Обзор 1even Platform](for-people/1even-platform-overview.pdf) | PDF, 12 страниц |
| ИИ-агент | [`AGENTS.md`](AGENTS.md), затем [`for-agents/overview.md`](for-agents/overview.md) | Markdown |

Если вы даёте этот репозиторий агенту (Claude Code, Codex, Cursor), укажите ему на
`AGENTS.md`. PDF агенту читать не нужно: тот же текст лежит в `for-agents/`.

## Что в обзоре

- зачем платформа нужна командам, которые уже пользуются ИИ-агентами;
- что агент делает для аналитиков, инженеров данных, разработки, финансов и безопасности;
- шесть сценариев: вопросы по данным, инциденты, отчёты, изменения, память команды,
  настройка без разработчика;
- модель доступа и то, что записывается в журнал;
- две схемы: как проходит запрос и как устроена память;
- с чего начать пилот и какие у текущей версии ограничения.

## Структура

| Папка | Содержимое |
|---|---|
| [`for-people/`](for-people/) | Обзор в PDF |
| [`for-agents/`](for-agents/) | Тот же обзор в Markdown, с текстовым описанием схем |
| [`diagrams/`](diagrams/) | Схемы в SVG: [путь запроса](diagrams/request-path.svg), [память](diagrams/memory.svg) |

Документы описывают платформу версии 0.21.0. Фреймворк CAPTURE, по которому лаборатория
внедряет агентную аналитику, лежит в отдельном репозитории `1even-lab/capture-framework`.

## Лицензия

Тексты и схемы в этом репозитории распространяются по лицензии Creative Commons
Attribution-ShareAlike 4.0 International (CC BY-SA 4.0), полный текст в файле
[`LICENSE`](LICENSE). Их можно использовать, распространять и перерабатывать, в том числе
в коммерческих целях, если указан источник, а переработанная версия распространяется под
той же лицензией.

Указание авторства: 1even Platform documentation by Max Ivanov, 1even.lab
(github.com/1even-lab/docs), CC BY-SA 4.0.

Код платформы распространяется отдельно, под лицензией MIT.

---

## In English

Documents from 1even.lab about 1even Platform, a self-hosted platform that runs an AI
agent on top of a company's data stack. The overview comes in two forms: a
[PDF for people](for-people/1even-platform-overview.pdf) and
[Markdown for AI agents](for-agents/overview.md). Agents start at [`AGENTS.md`](AGENTS.md).
The overview is written in Russian.

The text and diagrams are licensed under CC BY-SA 4.0. Suggested attribution: 1even
Platform documentation by Max Ivanov, 1even.lab (github.com/1even-lab/docs), CC BY-SA 4.0.
