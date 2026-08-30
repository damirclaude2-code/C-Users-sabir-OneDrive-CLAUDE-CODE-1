# Open-Source Stack

Этот pack не опирается на платные UI kits.

Для web-задач `Tailwind CSS`, `shadcn/ui`, `daisyUI` и `HyperUI` считаются default
бесплатным style baseline. Это не значит, что Claude Code обязан сразу ставить
npm-библиотеки. Это значит, что стиль, anatomy и block logic по умолчанию
берутся из этих бесплатных источников, если пользователь не попросил другой
визуальный direction.

Важно: `Tailwind CSS` - бесплатный open-source framework. `Tailwind Plus` -
платный коммерческий набор компонентов и шаблонов. В этом pack разрешен только
бесплатный `Tailwind CSS`, а `Tailwind Plus` запрещен.

Если проект использует компонентный веб-стек, Claude Code может
использовать следующие бесплатные источники как ориентир или как code-level
baseline:

## 1. Tailwind CSS

- роль: бесплатная utility-first CSS база для web UI;
- лицензия: MIT;
- сильная сторона: быстрый styling baseline для `shadcn/ui`, `daisyUI` и
  многих free UI patterns.

Запрещено путать с `Tailwind Plus`.

## 2. shadcn/ui

- роль: качественные primitives и registry-подход;
- лицензия: MIT;
- сильная сторона: copy-own-code модель, прозрачная структура компонентов.

Подходит, когда нужны:

- базовые UI primitives;
- dialogs;
- tabs;
- accordions;
- form patterns.

## 3. HyperUI

- роль: marketing blocks;
- лицензия: MIT;
- сильная сторона: hero, CTA, footer, FAQ, layout sections.

Подходит, когда нужны:

- hero patterns;
- CTA sections;
- footer patterns;
- marketing structure.

## 4. daisyUI

- роль: быстрый theme-aware utility baseline;
- лицензия: MIT;
- сильная сторона: быстрые theme classes и понятный старт для Tailwind-проектов.

Подходит, когда нужно:

- быстро показать theme direction;
- ускорить прототип без paid kit.

## Что запрещено

- Tailwind Plus;
- Tailwind UI paid templates;
- Flowbite Pro;
- платные Figma/UI kits;
- любые component packs, которые пользователь не сможет использовать бесплатно.

## Что важно

Для новичков эти библиотеки должны устанавливаться автоматически в совместимый
веб-проект, если style-risk низкий.

Но этот pack не обязывает ставить npm libraries в любой репозиторий.

Если проект:

- не на Tailwind;
- не на React;
- не на Astro;

то Claude Code все равно может использовать этот pack как:

- систему выбора блоков;
- visual rules baseline;
- каталог skeleton templates.

Если пользователь явно говорит не использовать этот style baseline, следуй
`style-override-policy.md`.

## Auto-install policy

- `web_no_design_system` -> ставь бесплатный stack: `Tailwind CSS` при
  необходимости, `shadcn/ui` и `daisyUI`;
- `web_with_existing_design_system` -> сначала uplift plan;
- `web_unclear` -> сначала спросить или предложить plan;
- `not_web_project` -> не создавать web stack насильно.

## Когда реально стоит ставить библиотеку

Только если:

- стек проекта это поддерживает;
- пользователь действительно делает компонентный продукт;
- нужна code-level реализация, а не только структурный дизайн.

Иначе достаточно самого pack-а.
