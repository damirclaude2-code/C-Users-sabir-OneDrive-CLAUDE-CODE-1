# Proof loop routing

Use this rule to decide when a general instruction should activate proof loop.

## Direct triggers

Always consider proof loop when the user says:

- proof loop
- пруфлуп
- используй proof loop
- докажи перед готово
- проверь свежим verifier
- fresh verifier
- spec -> build -> evidence -> verify -> fix

## General orchestration triggers

When the user says one of these phrases, do not automatically launch proof loop for every small task. First evaluate task risk.

Russian:

- используй навыки
- используй скиллы
- используй субагентов
- подключи агентов
- работай через агентов
- сделай надежно
- проверь перед готово
- не говори готово без проверки
- нужна проверка результата

English:

- use skills
- use subagents
- use agents
- verify before done
- prove before done
- make it reliable
- use a verifier

## Risk gate

Activate proof loop when at least one condition is true:

- the task touches 3 or more files;
- the task changes production, deploy, automations, payments, credentials, integrations, or user-facing behavior;
- the task needs build, tests, screenshot, curl, diff, checklist, or another objective proof;
- the user is asking for a fix after previous attempts failed;
- the task changes prompts, agent behavior, MCP/tools, workflow routing, or rules;
- a wrong result would cost meaningful time, money, reputation, or data safety.

Do not activate proof loop when the task is:

- a simple question;
- a small read-only search;
- a one-line low-risk edit;
- a quick draft where evidence is not needed;
- a tiny documentation edit with no behavioral impact.

## Required behavior when activated

Run the flow:

1. spec
2. build
3. evidence
4. fresh verifier
5. fixer if needed
6. fresh verifier again until PASS or 3 fix attempts

Do not say "done" until verifier returns PASS for all acceptance criteria.

## Связь с Agentic Triage

Это не отдельный, конкурирующий механизм: `agentic-triage` (см. раздел `CLAUDE.md`)
уже делает первичную оценку риска для каждой нетривиальной задачи. Proof loop —
это то, что происходит на шаге "если риск средний/высокий — после изменений
нужен proof/check" из этой оценки. Сначала триаж определяет риск, затем (если
риск это оправдывает) включается proof loop.
