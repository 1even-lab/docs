<!-- Text version of the 1even Platform overview. For people: for-people/1even-platform-overview.en.pdf. -->

# 1even Platform: an AI agent for every team

A self-hosted platform for AI agents on top of a company's data stack.

It is deployed in your infrastructure and connects to your DWH, Airflow, git, Slack and other systems. The agent answers questions about data, diagnoses pipeline failures and prepares changes. It acts within the user's permissions; changes to code, data and settings are applied after approval.

**[WHERE IT RUNS]**

On your server, in Docker Compose. You choose the model. MIT licence.

**[WHOSE PERMISSIONS]**

The permissions of the person asking. If someone has no access to a table, the agent will not read it.

**[HOW IT WRITES]**

It changes nothing on its own. It prepares a change and waits for a person with write access to approve it.

Why it matters

## Teams already use AI agents, and each team has its own

The analyst has an agent in the IDE, the on-call engineers set up a Slack bot, the product manager uploads exports into a chat. All of this is useful. The problems start when such an agent becomes part of a working process.

### Recurring work depends on one laptop

A morning digest or a weekly report runs from one employee's client, on their tokens. While they are on holiday the report does not arrive, and nobody knows how to restart it.

### The bot shows data to people who should not see it

The bot queries the warehouse under a shared service account, so it answers anyone who asks and the whole channel sees the reply. The warehouse logs show the same login every time, so there is no way to tell who requested the data.

### The agent does not know the rules the team knows

A mandatory filter, a correction to a metric, tables that must not be joined directly. All of this lives in people's heads and in old threads. The agent does not know it and returns a number that looks right.

### Nobody reviews the agent's changes

If the agent has write access, it changes code, data or configuration without review. Later it is hard to tell what changed and at whose request.

Employees already use agents; the company's job is to make that work manageable. 1even Platform provides a shared permission model and a shared audit log for it.

What 1even Platform is

## The agent runs on the company's server and follows its access rules

The platform connects to the systems you already have: warehouse, orchestrator, git, wiki, tracker, messenger. Interactive requests run with the user's permissions; scheduled tasks run under the project role. Everything the agent does is logged.

How people work with it

### Slack

Ask in a channel or in a direct message. Each channel has a set purpose: answering questions, delivering reports or watching alerts.

### Web UI

Chat, proposals waiting for approval, reports, schedules, access management.

### Claude Desktop, Claude Code, Codex, Cursor

They connect to the platform as a tool server. The model reasons on the user's side; permissions and keys stay on the platform.

### Schedules and alerts

A task starts without a person. The result arrives in a channel or a direct message.

Four rules built into the architecture

### All external calls go through one gate

Permissions are checked before every call. The key is injected on the server and the call is logged.

### Changes are applied after approval

The agent writes a proposal. A person with write access to the project approves it, and the executor applies exactly that version. Code changes go out as a Draft MR.

### Each project has its own perimeter

Data sources, metrics, channels, warehouse roles and keys are set per project. If a request has no project, the platform refuses it.

### Knowledge goes through review

A record proposed by the model becomes usable after a person approves it. For each task the agent receives a small selection of that knowledge.

Teams

## What the agent does for different teams

The platform and the permission model are shared. Projects differ: each team has its own sources, metrics and channels.

| Team | How they work today | Where it breaks down | What the platform adds |
| Analysts | Claude Code or Cursor connected to the DWH, with their own skills. | Everyone has their own formulas and skills, access runs on personal keys, results stay on the laptop. | A shared metric catalogue and skills from git, queries under a personal account, reports published on the platform. |
| Product and business | They ask a Slack bot or upload an export into a chat with a model. | The bot runs under a service account; the export goes stale. | An answer from the DWH under their own permissions, with the query and the period. Metric subscriptions. |
| Data engineers and on-call | They go through the log with an agent in the IDE once they sit down to the incident. | The investigation starts in the morning; context is gathered by hand. | The investigation starts from the alert; the fix arrives as a Draft MR for approval. |
| Development | AI review in the IDE or in CI. | The reviewer does not know the data conventions or the team's past mistakes. | Review that uses project memory, with comments in the MR itself. |
| Finance and restricted areas | Agents are not connected: the data is too sensitive. | The team is left without a tool. | A separate project with its own roles; rows go to direct messages only. |
| Head of data | Hears about agents in conversation. | No view of who uses what, or whether it helps. | An audit log of calls and an outcome review for each task. |
| Security and IT | They allow agents case by case or ban them. | Keys sit on laptops; the agent's actions are invisible. | Keys in Vault, sign-in through SSO, every action logged. |

**[How a new team is connected]**

- An administrator creates a project and lists its data sources.

- The project owner describes the metrics and adds Slack channels.

- Members get an access level: read or write.

- The team asks its first questions and writes missing rules into project memory.

A team can describe a new scenario itself, from chat or from Claude. Before it goes live it is checked with a dry run and approved by an administrator.

Scenarios

## Data questions and incidents

Answers to data questions

### An employee asks in Slack and gets a number with the query behind it

Today

The question goes to an analyst and waits in the queue. The answer comes the next day, usually as a single number. Ask another analyst the same question and the number may differ.

With the platform

The agent answers in the same thread. The number comes with the SQL query, assumptions, period and filters, so the answer can be checked. The metric formula is defined once in the catalogue, so every calculation uses the same definition.

How it worksThe agent picks a metric from the catalogue and the slice it needs; the metric layer builds the query and adds the mandatory filters and corrections itself. If the catalogue has no such metric, the agent writes SQL with read-only access. The query runs under the asker's role. Rows from the warehouse reach a shared channel only if the channel is marked for them.

`product` `business` `analysts` `query_metric`

Incident investigation

### When a pipeline fails, the investigation appears in the alert thread

Today

The alert arrives at night and sits until morning. In the morning the on-call engineer opens the log, looks for the last commit and checks the load on the warehouse. That is how the working day starts.

With the platform

By the time the engineer opens the thread, it already holds an incident card: what failed, the likely cause, the evidence and the proposed fix. The engineer checks the investigation and approves the fix.

How it worksAn alert from a trusted bot starts the agent with a diagnostic set of tools. All of them are read-only: orchestrator runs and logs, repository history, warehouse diagnostics. The agent files the fix as a proposal. After approval it becomes a Draft MR or a tracker task. The agent deploys nothing to production.

`data engineers` `on-call` `Airflow` `GitLab`

Scenarios

## Reports and changes

Reports and schedules

### Reports and digests run on the server and are published on the platform

Today

One employee runs the digest from their own client. An HTML dashboard built by an agent is passed around as a file. Such a report has no address, no access control and no version history, and building a separate BI dashboard for it is not worth it.

With the platform

The schedule lives on the server. A report opens as a page on the platform, and access follows the project level. Every version has an author, and the previous one can be restored. Reports export to PDF and CSV.

How it worksThe simplest option is an answer delivered to a channel on a schedule. A permanent report gets a folder in the project repository with its queries and page, reviewed through an MR. The report's queries run with the permissions of whoever opens it. If a scheduled run produced no answer, recipients get nothing and the owner gets a message with the reason.

`analysts` `business` `metric_digest` `report_build`

Changes to code and data

### The agent prepares a change; the executor applies it after approval

Today

If the agent may not write, a person does all the work after the diagnosis. If it may, changes appear without review.

With the platform

The agent takes the task as far as a proposal with a diff and a rationale. A person with write access to the project answers yes or no in the thread. The version they saw is the one applied. Who approved it and when is stored in a separate table.

How it worksThe agent has no write tool, only tools for proposals. After a proposal the task pauses. When approval arrives, the executor applies the proposal without calling the model again, and first checks that the source file has not changed. Code changes open as a Draft MR. The agent reviews other people's MRs the same way and posts its comments.

`development` `data engineers` `Draft MR` `approvals`

Scenarios

## Team memory and configuration

Team memory

### Rules for working with data are stored in the project and reach the agent together with the data

Today

Two or three people know how a metric is calculated and what caveats a table has. Part of it is written down in old threads. The agent does not see these rules and repeats mistakes the team has already worked through.

With the platform

The project has a memory: facts, a glossary, conventions, reviewed mistakes. A record can be bound to a table, a metric or a value. It then reaches the agent every time an answer touches that object.

How it worksPeople add records, some are imported from the wiki and the repository, and some the agent proposes itself after finished tasks. Whatever the model proposes goes into a review queue. Duplicates and noise are filtered out automatically; a person approves the rest. A small block of knowledge is assembled for each task. Mandatory conventions and bound records are passed in full. The log shows exactly what the agent received.

`all teams` `memory` `skills from git`

Configuration without a developer

### A new report, schedule or channel is added through settings

Today

To add a report or connect a channel, the team files a task for developers and waits for a release.

With the platform

An employee describes what is needed in chat or in Claude. The platform does a dry run and shows the result. An administrator approves the proposal in the Inbox, and it starts working.

How it worksProjects, connections, agent prompts, metrics and schedules are stored as configuration. Changes from users follow the same path as the agent's writes: a proposal first, then approval. Industry logic lives in plugins. There is a pack for iGaming today: game catalogue ingestion, dictionary normalisation, industry corrections to metrics.

`head of data` `analysts` `propose_binding` `dry_run_task`

For the security team

## The agent gets the permissions of the person who asked

A tool call goes through when three checks allow it at once. If the person, their role or their project level is not defined, the call is refused.

**[CHECK 1]**

### The agent's tool set

It is set by where the request came from. The text of the request does not affect it, so asking the agent to pick up another tool will not work.

**[CHECK 2]**

### The person's role

The organisation role defines the classes of operations. If an unknown role is configured, the person gets minimal permissions.

**[CHECK 3]**

### The project level

Three values: no access, read, write. A project where nobody has a level is closed to everyone except the administrator.

### Warehouse queries

When someone connects from Claude, the query runs under their personal account. Their grants and row policies apply, and the warehouse logs show their login. If the person has no warehouse role, the query is refused, for an administrator too.

### Data in shared channels

In direct messages, data is available within the user's permissions and the limits of the source. The agent sends warehouse rows to a channel if the channel is marked for such data, belongs to the same project and Slack confirms it is internal.

### Keys

The agent only sees key names. The key value is not passed to the model; the server injects it when the call is allowed. It does not appear in answers, logs or traces.

### Accounts and roles

Sign-in goes through corporate SSO. Accounts, roles and project levels can be synchronised with directory groups. If the directory is unavailable, the platform changes nothing. If a person is removed from a group, access is revoked.

### Audit log

Each call records who started it, which agent ran it and what changed. Approvals are stored in a separate table.

### Model

The model is connected through LiteLLM, and a local one can be used. With a cloud model the task context is sent to its provider, which is worth keeping in mind when choosing.

## How a request travels

A request from any source goes through the same stages: sign-in, permission check, execution, calls to external systems through the gate.

## How memory works

A record becomes usable after review. The agent receives the part of memory the task needs.

Alternatives

## Compared with how agents are used today

Typical configurations without extra engineering are compared: an agent in the IDE on an employee's machine, a bot with one service account, a cloud agent by subscription. Specific products and settings may give a different result.

|  | Agent in everyone's IDE | Bot on a service account | Cloud SaaS agent | 1even Platform |
| Works when the person is away | depends on setup | yes | yes | yes |
| Reads data with the asker's permissions | yes | depends on setup | depends on setup | yes |
| Data and keys stay inside the company | partly | yes | depends on product | yes |
| Writes require a person's approval | depends on setup | depends on setup | depends on setup | yes |
| Shared metrics and knowledge for all teams | no | partly | partly | yes |
| Audit log: who, and on whose behalf | local, on the laptop | depends on setup | at the vendor | yes |
| Choice of model, including a local one | partly | yes | depends on product | yes |
| A new scenario without development | for one employee | no | within the product | yes |

**[What the platform does not replace]**

Claude Desktop and Claude Code remain the employee's working tool. The platform adds permission-checked access to data and the team's shared knowledge.

BI dashboards stay where they are. The platform covers questions that have no dashboard and hosts reports that are not worth building in BI.

The decision to merge still belongs to the engineer.

Where to start

## You can start with a pilot on one team

The platform tracks outcomes: a task is tied to a goal and a person accepts the result. When the pilot ends you will have a report on how many tasks were completed and accepted.

**[Stages]**

- Installation. Docker Compose on your Linux host, a model connection, the first administrator.

- Connecting systems. SSO, warehouse, orchestrator, git, wiki, Slack. Keys go into Vault.

- First project. A data map, five to ten metrics, channels, access levels.

- Three scenarios. Answers to data questions, a morning digest, alert investigation.

- Results. A report on the outcomes and a decision on which teams to connect next.

**[What we need from you]**

- A Linux server in your network and access to a model

- A team that will use the agent, and a project owner

- Service accounts for your systems with read access

- An employee with write access who will approve proposals

**[What the platform works with today]**

ClickHouse and DuckDB, Airflow, GitLab, Outline, Asana, Slack, Entra ID and Keycloak.

**[Limits of the current version]**

- Slack is the only supported messenger. Reports are also available in the web UI, with export to PDF and CSV

- The OAuth gateway for Claude Desktop is in development

- For now the 1even.lab team carries out the installation

Next step

### Let's discuss a pilot for your team

Pick one team and three tasks it handles regularly. At the meeting we will go through how the agent handles them and what needs to be connected for a pilot.

Code and installation guide: github.com/1even-lab/

## Diagram "How a request travels": contents

File: `diagrams/request-path.en.svg`.

- Request
- People
- web UI
- Unattended
- schedule
- alert
- The model may run on the client side. Permissions and the audit log always stay on the platform.
- Perimeter
- Sign-in
- Corporate SSO. MFA and device policy stay with you.
- Token
- Opens one plane: REST, /mcp or a project runner.
- Network
- The platform is reachable from your network or through a tunnel.
- 1even Platform · inside your network
- Who is asking
- Organisation role
- Project level
- Both the role and the level are required.
- Warehouse role
- Warehouse grants decide which rows come back.
- Deny by default
- No person, project or level: the call is refused.
- How the work runs
- Mode 1
- Conversation loop
- A manager agent with read tools: metrics, SQL, pipeline logs, wiki, repository. It cannot write; it can propose.
- read
- approval
- executor
- Mode 2
- Graphs
- Fixed workflows: analysis, reports, digests, data quality checks, syncs.
- Mode 3
- Router /mcp
- The client's model does the reasoning. The platform checks permissions, injects keys and returns data together with the knowledge about it.
- Gate
- permissions on every call
- the project the call touches
- key from Vault, server-side
- audit log entry
- The agent sees key names. Values never reach the model.
- Knowledge
- What the agent knows before it answers
- The project data map, metric catalogue, memory and skills. A small block is assembled for each task. Records proposed by the model are approved by a person.
- Audit log
- What is recorded
- Agent steps, tool calls, approvals and outcome reviews.
- knowledge for the task
- every call
- Your systems
- Reads run directly. Writes run after a person approves.
- the answer comes back: chat thread · Slack channel · direct message · PDF · report page
- How a request travels through 1even Platform

## Diagram "How memory works": contents

File: `diagrams/memory.en.svg`.

- Sources
- A person
- Writes in the UI, from chat or from Claude. Before saving, the platform looks for similar records.
- Active at once
- Review of a finished task
- The model reads the conversation and extracts up to five records worth keeping.
- Candidate only
- Wiki
- Pages from an allowlist are imported. The platform does not read the rest.
- Repository
- Team conventions, skills and metric definitions as code.
- Warehouse
- Tables and their comments become the data catalogue. It is a map of what exists, kept apart from memory.
- Review
- Daily check
- Duplicates and noise are removed automatically. The remaining records get an automatic preliminary verdict: accept, reject, unsure.
- A person decides
- A record is approved by someone with the data_steward role. That role cannot run tasks.
- Can it leave the project
- Not by default. Only procedures, lessons, conventions and skills can be portable.
- Project memory
- Record type
- Who can read
- one person · project · whole company
- State
- The agent only receives records in the active state.
- Binding
- A record can be bound to a table, a metric or a value. It then comes with every answer that touches them.
- Provenance
- Source, task, owner and a hash of the text.
- Retrieval for a task
- What goes into the block
- project data map
- project knowledge
- company knowledge
- How it is selected
- The words of the question, the agent and tool, and semantic similarity all count. The access filter runs before ranking.
- Always passed in full
- Bound records and mandatory conventions. Without them the answer would be wrong.
- Size limit
- The block has a hard limit. Skills go in as pointers and their text loads on request. Conversations are never included.
- Who receives it
- Platform agents
- The block arrives with the task, before the answer starts.
- Claude over /mcp
- Searches memory, loads a skill, saves a conversation as a candidate.
- Data tools
- Return rows together with the records that explain them.
- Project router
- Uses the data maps to decide which project a question belongs to.
- a person's record goes straight into memory, skipping the queue
- Knowledge pack
- The only way out
- An administrator exports only approved, portable, company-level records. A filter checks each one again for project names. If the filter cannot build the list of names, the export does not run.
- Telemetry
- What the agent was shown
- Each retrieval records what was offered and what was loaded. Selection quality is tested against a reference set of questions.
- every retrieval
- a finished task yields new candidates
- How memory works in 1even Platform
