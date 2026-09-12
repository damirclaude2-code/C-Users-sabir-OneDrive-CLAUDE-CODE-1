# LLM Gateway — две дорожки для разных задач

Зачем это нужно: не все задачи, которые решает Claude Code или автоматизации
(например n8n), одинаково сложные. Простая классификация текста или JSON-ответ
не должны стоить так же дорого и требовать той же модели, что сложная задача
вроде архитектурного решения или финальной редактуры важного текста. Разделение
на две дорожки экономит деньги и держит качество там, где оно реально нужно.

```text
SIMPLE задачи → бесплатный пул ключей → часто и быстро
COMPLEX задачи → Claude/Codex CLI по подписке → редко, но качественно
Снаружи → один OpenAI-compatible формат
```

## Что лежит в этой папке

| Файл | Что внутри |
|---|---|
| [`simple-gateway-plan.md`](simple-gateway-plan.md) | Архитектура SIMPLE gateway — бесплатные ключи Gemini/Groq через LiteLLM Proxy |
| [`complex-cli-gateway-plan.md`](complex-cli-gateway-plan.md) | Архитектура COMPLEX gateway — Claude Code CLI / Codex CLI через плоские подписки |
| [`routing-dictionary-ru.md`](routing-dictionary-ru.md) | Русский словарь триггеров: когда задача идёт в SIMPLE, когда в COMPLEX |
| [`credentials-checklist.md`](credentials-checklist.md) | Какие ключи нужны и где их взять |
| [`litellm-config.example.yaml`](litellm-config.example.yaml) | Пример конфига LiteLLM Proxy (без реальных ключей) |
| [`local-env.example`](local-env.example) | Пример `.env` для gateway (без реальных ключей) |

## С чего начать

1. Зарегистрировать бесплатные ключи для SIMPLE-дорожки:
   - Gemini: <https://aistudio.google.com/apikey>
   - Groq: <https://console.groq.com/keys>
2. Прочитать [`credentials-checklist.md`](credentials-checklist.md) и вставить полученные ключи в чат — они сразу уйдут в локальный `credentials.md` (в git не попадают).
3. Прочитать [`simple-gateway-plan.md`](simple-gateway-plan.md), если нужна SIMPLE-дорожка, или [`complex-cli-gateway-plan.md`](complex-cli-gateway-plan.md), если нужна COMPLEX.
4. Посмотреть [`routing-dictionary-ru.md`](routing-dictionary-ru.md) — по этому словарю Claude Code сам определяет, в какую дорожку отправлять задачу.

Это план и документация, а не готовый к запуску сервис — сам LiteLLM Proxy
или internal CLI gateway нужно будет развернуть отдельно, когда дойдёт до
реального использования.
