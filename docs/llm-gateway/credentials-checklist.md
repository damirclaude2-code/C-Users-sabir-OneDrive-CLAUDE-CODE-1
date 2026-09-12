# Чеклист ключей для LLM Gateway

Где регистрировать:

```text
Gemini API key: https://aistudio.google.com/apikey
Groq API key: https://console.groq.com/keys
OpenRouter API key (optional): https://openrouter.ai/settings/keys
```

Официальная документация, если понадобятся детали:

- Gemini API key docs: <https://ai.google.dev/gemini-api/docs/api-key>
- Groq Quickstart: <https://console.groq.com/docs/quickstart>
- OpenRouter API key docs: <https://openrouter.ai/docs/api-keys>

## Что может понадобиться

| Секрет | Для чего | Обязателен? |
|---|---|---|
| Gemini API key | Основной provider SIMPLE-дорожки | Да, для SIMPLE |
| Groq API key | Fallback-provider SIMPLE-дорожки | Да, для SIMPLE |
| OpenRouter API key | Доп. fallback (free-tier) | Нет, опционально |
| LiteLLM master key | Доступ к самому LiteLLM Proxy | Да, для SIMPLE |
| Internal CLI gateway token | Доступ к COMPLEX gateway извне (например из n8n) | Только если gateway вызывается не только с этого компьютера |
| Hostname/адрес gateway | Куда стучаться клиенту (например n8n) | Да, если gateway используется вне этого компьютера |
| Отдельный ключ для n8n | Если n8n вызывает gateway напрямую | Только если есть такой сценарий |

## Где реально хранится значение

```text
Gemini API key: хранится в credentials.md как GEMINI_API_KEY
Groq API key: хранится в credentials.md как GROQ_API_KEY
LiteLLM master key: хранится в credentials.md как LITELLM_MASTER_KEY
```

Реальные значения в этом файле и в остальной документации никогда не
записываются — только имена переменных. Сами значения живут в
[`credentials.md`](../../credentials.md) (корень репозитория, защищён
`.gitignore`, в GitHub не попадает).

**Как добавить ключ**: просто вставь его в чат — я перенесу в `credentials.md`
и не буду печатать значение обратно.
