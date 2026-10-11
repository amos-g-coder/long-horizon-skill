# Long Horizon

Long Horizon is an agent skill for turning an ambitious Codex Goal mode request into a compact execution contract, then carrying it through milestones and context cycles. It keeps the original objective, records durable state when needed, validates each milestone, and stops at explicit safety or completion boundaries.

## Install

The skill lives in [`skills/long-horizon`](https://github.com/amos-g-coder/long-horizon-skill/tree/main/skills/long-horizon). The repository is public, so any agent can download or clone it without a GitHub account.

### Codex skill installer

Ask Codex to install this skill from:

```text
https://github.com/amos-g-coder/long-horizon-skill/tree/main/skills/long-horizon
```

If you use Codex's built-in installer script:

```sh
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo amos-g-coder/long-horizon-skill \
  --path skills/long-horizon
```

Restart or begin a new Codex turn after installation so the skill is discovered.

### Manual installation

```sh
git clone https://github.com/amos-g-coder/long-horizon-skill.git
mkdir -p ~/.codex/skills
cp -R long-horizon-skill/skills/long-horizon ~/.codex/skills/
```

For another agent runtime, copy the complete `skills/long-horizon` directory into its skills directory. The instructions refer to Codex Goal mode, so other runtimes may need to adapt that workflow.

## Use

Invoke `$long-horizon` with a concrete objective in Codex Goal mode. The skill is intended for autonomous work that may span days or multiple context cycles.

## Files

- [`SKILL.md`](skills/long-horizon/SKILL.md): execution workflow and guardrails
- [`references/durable-state.md`](skills/long-horizon/references/durable-state.md): contract and state templates
- [`agents/openai.yaml`](skills/long-horizon/agents/openai.yaml): Codex display metadata

## License

MIT. See [LICENSE](LICENSE).
