# Numerology Analysis Skill

这是一个给 Claude Code、Codex 这类 Agent 工具使用的通用 Skill 包。

现已作为独立 skill 安装在 `.claude/skills/numerology-analysis/`（与组合命理 skill `yuan` 分离），
这样用户只问数字命理时，不需要先走 `yuan` 的六法完整入户流程（姓名/性别/出生时间/出生地/历法）。
`yuan/references/numerology/` 下仍保留原始参考包，供 `yuan` 内部六法分析引用。

## 设计定位

- **运行时 Skill 名称**：`numerology-analysis`
- **内部规范 ID**：`numerology_analysis`
- **能力范围**：根据姓名与出生日期，计算生命路径数与姓名数，并按固定符号映射输出结构化 JSON
- **限制**：只做纯符号映射，不做事件预测、吉凶判断，也不输出医学 / 法律 / 金融结论

之所以把运行时名称写成 `numerology-analysis`，是为了兼容更严格的 Skill 名称规则；而 `numerology_analysis` 保留在机器可读规范里作为内部 ID。

## 文件说明

- `SKILL.md`：主 Skill 文件，Claude Code / Codex 都可读（含 trigger、sequence canon、anti-patterns、gate、self-check、与 `yuan` 的区分规则）
- `assets/spec.json`：机器可读 Skill 规范
- `assets/output.schema.json`：输出 JSON Schema
- `assets/example_input.json`：示例输入
- `assets/example_output.json`：示例输出
- `agents/openai.yaml`：Codex 可选元数据

## 建议输入格式

```json
{
  "input": {
    "name": "张三",
    "birthdate": "1992-08-17"
  }
}
```

支持的生日格式：

- `YYYY-MM-DD`
- `YYYY/MM/DD`
- `YYYYMMDD`

若日期存在歧义（例如 `03/04/2001`），建议先改成 ISO 格式再调用。

## 示例结果

参见 `assets/example_output.json`。已人工核算：1992-08-17 → 生命路径数 1；姓名"张三" → 姓名数 4；两者符号标签与示例输出完全一致。
