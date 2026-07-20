# qa-skill

`qa-skill` is a Codex skill for structured requirement clarification. It guides Codex to ask one question at a time, update its understanding after each answer, and only produce a plan once the key requirements are sufficiently clear.

## When To Use

Use this skill when a task is ambiguous and should not jump straight into implementation, especially for:

- architecture or module design
- research-to-code translation
- algorithm integration
- large refactors
- planning before coding
- requirements that need user confirmation step by step

The intended interaction pattern is:

```text
question -> user answer -> next question -> user answer -> plan
```

Codex should move to the final plan when it understands roughly 80% of the important requirements and only minor details remain.

## Installation

Place this folder under your Codex skills directory:

```bash
cp -r qa-skill ~/.codex/skills/qa-skill
```

Then restart Codex if the skill is not detected in the current session.

## Usage

Mention the skill by name in your prompt:

```text
Use qa-skill to clarify this request one question at a time, then produce a plan once the important requirements are understood.
```

You can also use the `$` form:

```text
$qa-skill I want to add a new planning module. Ask me one question at a time before giving the implementation plan.
```

Chinese example:

```text
使用 qa-skill，先向我提问，一次只能问一个问题。等你对需求理解达到 80% 以上后，再给出实现方案。
```

## Expected Behavior

While clarifying, Codex should:

- ask exactly one question per turn
- prioritize high-impact unknowns first
- avoid multi-question lists
- avoid premature implementation plans
- continue asking until the design is mostly clear

After enough information is collected, Codex should provide:

- goal and non-goals
- confirmed assumptions
- proposed architecture or workflow
- concrete file/module changes when relevant
- validation plan
- remaining minor open points, if any

## Example

User:

```text
$qa-skill I want to integrate a new unknown-region partition algorithm into my robotics project. Ask before planning.
```

Codex:

```text
先确认一个点：

这个算法本次是只做旁路可视化验证，还是要直接参与现有决策流程？
```

Codex continues one question at a time. Once the requirements are clear, it produces the implementation plan.

## Files

```text
SKILL.md              Skill instructions loaded by Codex
agents/openai.yaml    UI metadata for skill lists and chips
README.md             Human-readable usage guide
```
