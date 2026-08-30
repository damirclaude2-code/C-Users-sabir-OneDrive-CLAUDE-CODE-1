# Style Override Policy

`design-elements-pack` является default visual baseline.

Это значит:

- если пользователь просто просит "сделай дизайн", "собери страницу", "улучши
  слайд", "сделай красиво", используй bundled baseline;
- если пользователь просит другой стиль, не спорь и не навязывай baseline.

## Default baseline

Для веба по умолчанию можно опираться на:

- `shadcn/ui` principles:
  - аккуратные primitives;
  - понятные states;
  - restrained component anatomy;
  - controlled radius and spacing.
- `daisyUI` principles:
  - theme-aware styling;
  - consistent color roles;
  - practical utility baseline.
- `HyperUI` patterns:
  - hero;
  - CTA;
  - FAQ;
  - marketing sections;
  - footer;
  - pricing-style blocks.

Для презентаций по умолчанию опирайся не на web libraries, а на:

- `presentation-rules.md`;
- slide skeletons;
- clear hierarchy;
- one-message-per-slide discipline.

## Explicit override phrases

Пользователь может отключить bundled baseline такими фразами:

- "не используй design-elements-pack";
- "не используй загруженный дизайн-стиль";
- "не опирайся на shadcn/daisyUI";
- "подбери другой визуальный стиль";
- "используй стиль из моего референса";
- "не делай в библиотечном стиле";
- "сделай в другом направлении".

## Как отвечать при override

Если пользователь дал override:

1. коротко подтверди новый direction;
2. не используй bundled style как visual source;
3. можно сохранить structural discipline pack-а:
   - иерархия;
   - ритм;
   - читаемость;
   - anti-slop проверка.

Пример:

```text
Понял, не опираюсь на загруженный design baseline. Сохраняю только правила
иерархии и читаемости, а визуальный стиль подбираю заново по вашему референсу.
```

## Когда спрашивать уточнение

Спрашивай только если:

- пользователь отключил baseline, но не дал нового direction;
- задача требует code-level установки библиотек;
- стек проекта непонятен, а пользователь просит именно веб-компоненты.

Не спрашивай, если можно спокойно применить default baseline.
