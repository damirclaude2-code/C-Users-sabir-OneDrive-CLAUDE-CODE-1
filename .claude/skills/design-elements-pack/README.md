# Design Elements Pack

Локальная design library для сборки структуры новых экранов, лендингов и
слайдов из готовых сильных паттернов. После установки — default visual
baseline проекта (можно отключить явным запросом, см.
`references/style-override-policy.md`).

## Структура пакета

```text
design-elements-pack/
├── SKILL.md
├── README.md
├── references/
│   ├── pattern-catalog.md        — 14 сильных блоков и когда они нужны
│   ├── pattern-selection.md      — как выбрать маршрут по типу артефакта
│   ├── presentation-rules.md     — правила для слайдов (не мини-лендинг)
│   ├── visual-rules.md           — визуальный baseline, anti-slop
│   ├── style-override-policy.md  — когда уважать другой стиль пользователя
│   ├── open-source-stack.md      — бесплатный веб-стек (Tailwind/shadcn/daisyUI/HyperUI)
│   └── sources-and-licenses.md   — источники и лицензии pack-а
└── templates/
    ├── pricing-page-skeleton.md
    ├── comparison-page-skeleton.md
    └── presentation-lesson-slide-skeleton.md
```

## Подходит для

- нового лендинга (cold/warm);
- pricing-страницы;
- comparison-страницы;
- обучающего или продающего слайда с нуля;
- любой ситуации "с чего начать структуру".

## Когда НЕ это

Если экран/слайд уже существует и его нужно улучшить — используй `designer`,
не этот навык.

## Примеры вызова

```text
Собери pricing-страницу для нашего продукта с помощью design-elements-pack.
```

```text
Нужен слайд-объяснение для урока — используй presentation skeleton из
design-elements-pack.
```
