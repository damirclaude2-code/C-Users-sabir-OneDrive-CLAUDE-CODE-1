---
name: numerology-analysis
description: Compute symbolic numerology from a person's name and birthdate using deterministic mappings only. Use for numerology / нумерология / число жизненного пути / числовой код имени / 数字命理 / 生命路径数 / 姓名映射 requests and structured numerology JSON. Do not use for predictive fortune-telling or non-symbolic advice; do not use for a combined multi-method destiny reading (see Distinction from `yuan` below).
---

# Purpose

Return a numerology analysis using only the symbolic rules in this skill. The result must be deterministic, reproducible, and limited to symbolic mappings.

## What this skill fixes

Without it, "numerology" requests tend to drift into invented, non-reproducible fortune-telling (different answer every time, mixed in with astrology/tarot/luck claims). This skill fixes that by making the calculation a fixed deterministic function of exactly two inputs (name, birthdate): same input always produces the same numbers and the same labels.

## Trigger

Use this skill directly (without pulling in `yuan`) when the request is narrowly about:

- "нумерология", "число жизненного пути", "число имени", "числовой код имени"
- "numerology", "life path number", "name number"
- 数字命理, 生命路径数, 姓名映射

Do not wait for full birth-chart intake (name/gender/birth time/birthplace/calendar type) — this skill only ever needs a **name** and a **birthdate**. If one is missing, ask only for the missing field.

# Accepted input

Accept either:

1. A JSON object:
   ```json
   {
     "input": {
       "name": "",
       "birthdate": ""
     }
   }
   ```

2. A natural-language request that clearly includes both a name and a birthdate.

If one field is missing, ask only for the missing field.
If the birthdate is ambiguous (for example `03/04/2001`), ask for ISO `YYYY-MM-DD` before computing.

# Sequence canon

Always execute in this exact order — never skip or reorder a step:

1. **Normalize** the birthdate to 8 digits.
2. **Reduce** using `reduce_number` wherever a reduction is required.
3. **Calculate** the life path number from the normalized birthdate.
4. **Normalize** the name (trim, strip punctuation, uppercase Latin letters, leave non-Latin scripts untransliterated).
5. **Map** every name character (Latin table, or Unicode-codepoint fallback for non-Latin/unmapped characters).
6. **Calculate** the name number from the mapped values.
7. **Map** both numbers through the symbolic personality table.
8. **Compose** the output JSON exactly per the output contract.

# Rules

## 1) Normalize birthdate

- Accept `YYYY-MM-DD`, `YYYY/MM/DD`, or `YYYYMMDD`.
- Remove all non-digit characters to produce `normalized_birthdate`.
- `normalized_birthdate` must contain exactly 8 digits.
- If the date cannot be normalized to 8 digits, request correction.

## 2) Reduce function

Use this deterministic reducer everywhere a reduction step is required:

```text
reduce_number(n):
  while n is not 11, 22, or 33 and n > 9:
      n = sum_of_digits(n)
  return n
```

This preserves the master numbers `11`, `22`, and `33`.

## 3) Life path number

Compute:

```text
life_path_number = reduce_number(sum(digits(normalized_birthdate)))
```

## 4) Normalize name

- Trim leading and trailing whitespace.
- Ignore spaces, hyphens, underscores, apostrophes, and common punctuation.
- Convert Latin letters to uppercase before mapping.
- Do not transliterate non-Latin scripts into Latin. Use the fallback mapping directly.

## 5) Name mapping

### Latin mapping

Use the following fixed mapping:

- `A J S = 1`
- `B K T = 2`
- `C L U = 3`
- `D M V = 4`
- `E N W = 5`
- `F O X = 6`
- `G P Y = 7`
- `H Q Z = 8`
- `I R = 9`

### Fallback mapping for non-Latin or unmapped characters

For every character that is not mapped by the Latin table:

1. Take the character's Unicode decimal code point.
2. Sum the digits of that decimal code point.
3. Reduce that sum to a single digit from `1` to `9` (do **not** preserve 11/22/33 at this per-character step — that preservation only applies to the final `life_path_number` / `name_number` reduction).
4. Use that value as the character mapping.

Example:
- Unicode code point `24352` -> `2 + 4 + 3 + 5 + 2 = 16` -> `1 + 6 = 7`

## 6) Name number

- Map every valid character after name normalization.
- Compute:

```text
name_number = reduce_number(sum(mapped_character_values))
```

## 7) Personality map

Use only this symbolic map:

- `1` -> 标签 `["独立", "主动", "开创"]`, 符号 `"起点型"`
- `2` -> 标签 `["协调", "敏感", "合作"]`, 符号 `"联结型"`
- `3` -> 标签 `["表达", "创意", "社交"]`, 符号 `"表达型"`
- `4` -> 标签 `["稳定", "秩序", "执行"]`, 符号 `"结构型"`
- `5` -> 标签 `["变化", "自由", "探索"]`, 符号 `"变化型"`
- `6` -> 标签 `["责任", "关怀", "和谐"]`, 符号 `"照护型"`
- `7` -> 标签 `["内省", "分析", "洞察"]`, 符号 `"思辨型"`
- `8` -> 标签 `["目标", "掌控", "成就"]`, 符号 `"成就型"`
- `9` -> 标签 `["理想", "包容", "完成"]`, 符号 `"完成型"`
- `11` -> 标签 `["直觉", "启发", "感召"]`, 符号 `"启发型"`
- `22` -> 标签 `["建构", "整合", "落地"]`, 符号 `"建构型"`
- `33` -> 标签 `["奉献", "滋养", "引导"]`, 符号 `"滋养型"`

# Output contract

Return JSON with exactly this top-level structure:

```json
{
  "核心数字": {
    "生命路径数": 0,
    "姓名数": 0,
    "主导数": 0,
    "辅助数": 0
  },
  "性格": {
    "生命路径": {
      "标签": [],
      "符号": ""
    },
    "姓名映射": {
      "标签": [],
      "符号": ""
    },
    "综合": {
      "标签": [],
      "说明": ""
    }
  }
}
```

## Output rules

- `主导数 = 生命路径数`
- `辅助数 = 姓名数`
- `生命路径` uses the symbolic map for `life_path_number`
- `姓名映射` uses the symbolic map for `name_number`
- `综合.标签` is the de-duplicated concatenation of `生命路径.标签` followed by `姓名映射.标签`
- `综合.说明` must be exactly:
  `以内在核心采用生命路径数的符号映射，以外在表达采用姓名数的符号映射`

# Constraints

- Pure symbolic mapping only.
- No event prediction.
- No luck, fate, or timing claims.
- No medical, legal, financial, or safety claims.
- Do not add astrology, tarot, zodiac, feng shui, MBTI, clinical psychology, or any external system.
- Do not infer real-world outcomes from the numbers.
- Do not add unsupported narrative beyond the provided labels and symbols unless the user explicitly asks for a short explanation.

# Anti-patterns

- Predicting events, luck, or timing ("this year you will…") — not this skill's job, ever.
- Mixing in astrology/tarot/feng shui/MBTI or any other system into the output.
- Preserving 11/22/33 during the per-character Unicode fallback step (step 5) — that preservation rule applies only to the final `life_path_number`/`name_number` reduction, not to individual character mapping.
- Transliterating a non-Latin name into Latin letters before mapping — always map non-Latin characters via the Unicode-codepoint fallback directly.
- Returning prose instead of the exact JSON contract when the user hasn't asked for an explanation.
- Silently guessing an ambiguous date format instead of asking for ISO `YYYY-MM-DD`.
- Pulling in the full `yuan` six-method intake (gender, birth time, birthplace, calendar type) when the user only asked for numerology.

# Formatting behavior

- Default to JSON only.
- If the user explicitly asks for an explanation, provide the JSON first and then a short explanation that stays fully consistent with the same mapping and constraints.

# Gate — what counts as a good result

Only treat the output as correct if all of these hold:

- `normalized_birthdate` is exactly 8 digits, derived only from the provided birthdate.
- `life_path_number` and `name_number` are each in `{1..9, 11, 22, 33}`, computed by literally following `reduce_number`.
- The JSON validates against `assets/output.schema.json` (no extra fields, all required fields present, enums respected).
- Re-running the same input produces byte-identical numbers and labels (determinism check).
- No content beyond the defined labels/symbols/explanation leaked into the output.

# Self-check before final

Before returning the result, verify in order:

1. Did I normalize the birthdate to exactly 8 digits?
2. Did I apply `reduce_number` correctly, preserving 11/22/33 only at the final step (not mid-calculation per character)?
3. For non-Latin name characters, did I use the Unicode-codepoint fallback instead of transliteration?
4. Does the output match the schema exactly, with `主导数`/`辅助数` mirroring `生命路径数`/`姓名数`?
5. Is the output free of predictive, astrological, or other-system content?

If any check fails, recompute before responding.

# Distinction from `yuan`

This project also has a combined destiny-reading skill `yuan`, which includes numerology (数字命理) as one of six methods (alongside 八字, 称骨, 紫微斗数, 西方占星, 吠陀占星).

- Use **`numerology-analysis`** (this skill) when the user asks only about numerology/life-path/name-number and gives just a name + birthdate.
- Use **`yuan`** when the user asks for a full destiny/fortune reading, mentions multiple methods (八字, 紫微斗数, 占星, 称骨), or asks for a five-year forecast — that flow needs the full intake (name, gender, birth date+time, birthplace, calendar type) and produces a different Chinese-style report structure (资料确认/称骨歌诀/结论/事业/财运/感情/五年断事/建议), not this skill's plain JSON contract.
- Do not run both for the same request unless the user explicitly asks for both a quick numerology JSON and a full destiny reading.

# Canonical machine-readable spec

The canonical internal spec id is `numerology_analysis`.
The runtime skill name is `numerology-analysis` for broad compatibility across agent tools.
Use `assets/spec.json` as the machine-readable reference when needed.
