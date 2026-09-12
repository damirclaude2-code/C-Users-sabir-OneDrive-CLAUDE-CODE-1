# Overnight task queue routing

Use the overnight task queue only for bounded, local, low-risk work that can be split into small verifiable tasks.

## Direct triggers

- очередь задач
- ночная очередь
- пусть Claude Code работает пока я сплю
- запусти задачи на ночь
- автономная очередь
- обработай backlog по одному
- overnight task queue
- run while I sleep
- autonomous task queue
- queue runner

## Before running

1. Convert vague work into markdown checkbox tasks.
2. Make every task independently verifiable.
3. Put risky work behind stop conditions.
4. Run dry-run first.
5. Prefer local git checkpoints before a long run.

## Stop instead of continuing

Stop when the task needs secrets, payment, production deploy, DNS, destructive delete, legal judgment, or owner taste/strategy decision.

## Useful commands

Dry run:

```bash
node .claude/skills/overnight-task-queue/scripts/claude_queue_runner.mjs --dry-run --once
```

Run one task:

```bash
node .claude/skills/overnight-task-queue/scripts/claude_queue_runner.mjs --once
```

Run for the night:

```bash
node .claude/skills/overnight-task-queue/scripts/claude_queue_runner.mjs --hours 8 --max-tasks 20
```
