---
name: overnight-task-queue
description: Plan and run a safe local Claude Code task queue for long unattended work. Use when the user asks to build an overnight queue, run tasks while away/asleep, process backlog items one by one, or install an autonomous queue runner with checkpoints, proof, git commits, stop conditions, and morning report.
allowed-tools: [Read, Write, Edit, Bash]
---

# Overnight Task Queue

Use this skill when work should be broken into a local queue and processed safely over time by Claude Code. The goal is not "let the agent do anything"; the goal is a bounded queue where each item is small, checked, and stopped if risk or ambiguity appears.

## Trigger phrases

Russian:
- очередь задач
- ночная очередь
- пусть Claude Code работает пока я сплю
- запусти задачи на ночь
- автономная очередь
- обработай backlog по одному
- поставь очередь для Claude Code
- продолжай задачи без меня

English:
- overnight task queue
- run while I sleep
- autonomous task queue
- process backlog one by one
- unattended Claude Code run
- queue runner

## Core rule

One queue item = one Claude Code invocation = one proof packet.

Never combine multiple queue items into one vague prompt. Never continue after an item fails unless the queue policy explicitly marks the next item safe and independent. Default behavior is to stop on failure or uncertainty.

## Workflow

1. Check whether the current folder is a local project and whether `claude` is available in `PATH`.
2. Create or update:
   - `.claude/queue/tasks.md`
   - `.claude/queue/logs/`
   - `.claude/queue/evidence/`
   - `.claude/skills/overnight-task-queue/scripts/claude_queue_runner.mjs`
3. Turn the user's backlog into small checklist items in `.claude/queue/tasks.md`.
4. Add constraints to the top of the queue:
   - no purchases;
   - no production deploys without explicit permission;
   - no broad deletes;
   - no secret exposure;
   - stop if credentials, payment, destructive migration, or owner judgment is required.
5. Run a dry check first:
   ```bash
   node .claude/skills/overnight-task-queue/scripts/claude_queue_runner.mjs --dry-run --once
   ```
6. For real work, run with a time budget:
   ```bash
   node .claude/skills/overnight-task-queue/scripts/claude_queue_runner.mjs --hours 8 --max-tasks 20
   ```
7. In the morning, inspect:
   - `.claude/queue/status.json`
   - `.claude/queue/logs/`
   - `.claude/queue/evidence/`
   - `git status`

## Stop conditions

Stop the queue and write a report when any of these happen:

- a task requires a secret, password, API key, payment, or account recovery;
- a task requires deleting many files or running a destructive migration;
- a task touches production deploy, DNS, billing, customer data, or legal wording;
- checks fail twice for the same reason;
- the project has unexpected unrelated dirty git changes;
- Claude cannot prove the acceptance criteria;
- the next task depends on an unresolved failed task.

## Runner

Use the bundled script:

```bash
node .claude/skills/overnight-task-queue/scripts/claude_queue_runner.mjs --help
```

The script processes the first open checklist item only, waits for it to be marked done by Claude, then moves to the next item. If Claude exits successfully but the item is still open, the runner treats that as uncertainty and stops.

## Proof packet

Each completed item should leave a small evidence file in `.claude/queue/evidence/` with:

- task text;
- files changed;
- checks run;
- result;
- remaining risks;
- git commit hash if a commit was created.

## Anti-Patterns (чего не делать)

- Не объединять несколько пунктов очереди в один расплывчатый промпт — один пункт = один вызов = один proof packet.
- Не запускать реальный прогон (`--hours`) без предварительного `--dry-run`.
- Не продолжать очередь после провала пункта, если политика очереди явно не разрешила следующий как безопасный и независимый.
- Не пускать в очередь пункты, требующие секретов, оплаты, продакшн-деплоя, DNS или юридических формулировок без стоп-условия.
- Не помечать пункт выполненным без evidence-файла в `.claude/queue/evidence/`.
- Не запускать длинную очередь без локальной git-точки сохранения перед стартом.

## Качество результата

Хороший результат — это когда:

- у каждого выполненного пункта есть evidence-файл с proof (что сделано, какие проверки прошли, что осталось рискованным);
- очередь сама остановилась на любом стоп-условии вместо того, чтобы продолжать через силу;
- `.claude/queue/status.json`, логи и `git status` согласованы — нет пунктов, помеченных done, без видимых изменений;
- утренний отчёт явно разделяет: что сделано, что пропущено и почему, что требует решения владельца.

## Быстрая проверка перед отдачей

- Был ли `--dry-run` перед реальным запуском?
- Есть ли git-точка сохранения до старта очереди?
- У каждого выполненного пункта есть evidence-файл?
- Не пропущено ли ни одно стоп-условие из списка выше?
