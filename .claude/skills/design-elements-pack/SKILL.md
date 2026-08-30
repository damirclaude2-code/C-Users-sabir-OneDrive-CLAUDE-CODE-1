---
name: design-elements-pack
description: Использовать, когда нужно быстро собрать структуру нового экрана, лендинга, слайда или сравнительной/тарифной страницы из готовых сильных паттернов — hero, proof, pricing, comparison, FAQ, CTA. Не для улучшения уже существующего визуального решения — для этого используй designer.
version: 1.0.0
status: local
allowed-tools: [Read, Write, Edit]
---

# Design Elements Pack

Ты работаешь как локальная design library, а не просто как ещё один "стиль
роли". Это installable pack: помимо этого файла, в проекте есть
`references/` (каталог паттернов, правила, политики) и `templates/`
(skeleton-структуры для типовых артефактов).

После установки этот pack становится **default visual baseline** для задач
про веб, экраны, презентации, схемы и визуальную упаковку — если пользователь
явно не попросил другой стиль (см. `references/style-override-policy.md`).

## Когда использовать

Используй этот навык, когда нужно собрать **структуру с нуля** из типовых
сильных блоков:

- новый лендинг (cold или warm);
- новая pricing-страница;
- новая comparison-страница;
- новый обучающий/продающий слайд;
- набор секций для экрана, которого ещё не существует.

Не используй `design-elements-pack` как первый выбор, если:

- артефакт уже существует и его нужно улучшить — тогда сначала `designer`;
- задача только про текст без структуры — тогда `copywriter`;
- нужна только проверка фактов — тогда `fact-checking`.

## Trigger

Подключай `design-elements-pack`, если в запросе есть сигналы:

- "собери лендинг";
- "сделай pricing страницу";
- "нужна comparison страница";
- "собери слайд с нуля";
- "какие блоки здесь нужны";
- "с чего начать структуру экрана".

## Локальная библиотека этого пакета

- `references/pattern-catalog.md` — каталог из 14 сильных блоков (Hero, Proof
  Strip, Problem/Solution, Value Props, Steps, Before/After, Comparison,
  Pricing, FAQ, Testimonial, Final CTA, Compact Table, Stats Showcase) —
  что каждый блок делает и когда нужен.
- `references/pattern-selection.md` — как выбрать маршрут: тип артефакта →
  главная задача → готовый route (cold landing, warm landing, pricing page,
  comparison page, sales slide, explanatory slide).
- `references/presentation-rules.md` — отдельные правила для слайдов: один
  слайд = одна главная мысль, один proof, один вывод; slide ≠ маленький лендинг.
- `references/visual-rules.md` — визуальный baseline: структура прежде
  красоты, дозированные акценты, чего избегать (generic gradients, card
  chaos, decorative без смысла).
- `references/style-override-policy.md` — когда и как уважать явный запрос
  пользователя на другой визуальный стиль.
- `references/open-source-stack.md` и `references/sources-and-licenses.md` —
  на какие бесплатные источники опираться для веба (`Tailwind CSS`,
  `shadcn/ui`, `daisyUI`, `HyperUI` — все MIT/бесплатные) и что запрещено
  (`Tailwind Plus`, платные UI/Figma kits).
- `templates/pricing-page-skeleton.md` — маршрут pricing-страницы.
- `templates/comparison-page-skeleton.md` — маршрут comparison-страницы.
- `templates/presentation-lesson-slide-skeleton.md` — маршрут обучающего/
  explanatory слайда.

## Sequence Canon

1. Определи тип артефакта (по `references/pattern-selection.md`):
   cold landing / warm landing / pricing page / comparison page / sales
   slide / explanatory slide / dashboard explainer.

2. Определи главную задачу: объяснить, снять непонимание, показать выгоду,
   доказать, снять возражения, сравнить, довести до действия.

3. Выбери маршрут блоков — если для артефакта есть готовый skeleton в
   `templates/`, используй его как основу, не изобретай структуру заново.

4. Собери маршрут из `references/pattern-catalog.md`. Для слайдов
   дополнительно проверь `references/presentation-rules.md` — слайд не
   лендинг, там обычно 3-4 блока максимум, а не полный marketing route.

5. Проверь style direction по `references/style-override-policy.md`:
   - если пользователь просто просит "сделай дизайн" / "собери страницу" —
     используй bundled baseline (shadcn/ui + daisyUI + HyperUI principles
     для веба, presentation-rules для слайдов);
   - если пользователь дал override-фразу — не навязывай bundled style,
     но сохрани структурную дисциплину (иерархия, ритм, читаемость).

6. Примени `references/visual-rules.md` при финальной сборке: дозируй
   акценты, не плоди одинаковые по силе карточки, оставляй воздух.

7. Для веб-задач с реальной code-level реализацией используй бесплатный
   стек из `references/open-source-stack.md` — Tailwind CSS / shadcn/ui /
   daisyUI / HyperUI. Установка npm-библиотек — отдельный шаг
   (`web-design-libraries-setup`), не часть этого навыка.

## Anti-Patterns

- изобретать структуру заново, когда в `templates/` уже есть готовый skeleton;
- собирать comparison page как "спор ради спора" вместо помощи в выборе
  (см. `references/comparison-page-skeleton.md`);
- вставлять pricing/FAQ-логику в слайд, где нужен один тезис
  (см. `references/presentation-rules.md`);
- делать 5 одинаково важных блоков подряд;
- использовать generic AI-эстетику (фиолетово-синие градиенты, bento-хаос);
- навязывать bundled baseline после явного override пользователя;
- путать этот навык с `designer` — этот собирает с нуля, `designer` правит
  существующее.

## Качество результата

Считай результат хорошим только если:

- выбран правильный тип артефакта и маршрут блоков;
- на каждом экране/слайде видно, что смотреть первым, вторым, третьим;
- различия в comparison/pricing считываются за секунды, без vague labels
  вроде "advanced features";
- слайды не превращены в лендинги внутри презентации;
- visual rules соблюдены (воздух, дозированные акценты, читаемая иерархия);
- override пользователя, если он был дан, реально уважен.

## Быстрая проверка перед отдачей

- Это структура с нуля (этот навык) или правка существующего (`designer`)?
- Использован ли подходящий skeleton из `templates/`, если он есть?
- Не превратился ли слайд в мини-лендинг?
- Сколько элементов реально борются за внимание — если убрать 30%, станет ли сильнее?
- Уважен ли явный style override, если он был?
