[简体中文](README.md) · **English**

# Character Card Skills

Chinese-language agent skills for writing and revising SillyTavern and BrainDance/taberna character cards and lorebooks. Use them to organize a character's motivations, opening scenes, world information, state, and memory. Local Python tools help inspect JSON and audit supported structures.

[Try a sample](#try-without-a-model-account) · [Install the skills](#install-the-skills) · [Writing guides](README.md#参考指南) · [Report a problem](https://github.com/Marco0431/character-card-skills/issues/new?template=bug_report.md)

This is a set of skills and utilities for creators, not a chat client. The writing guides are in Chinese. The agent performs creative work; the CLI tools read JSON and do not generate cards.

## Try without a model account

With Git and Python installed (validated with Python 3.12), run:

```sh
git clone https://github.com/Marco0431/character-card-skills.git
cd character-card-skills
python skills/campus-card-skill/scripts/query.py examples/worldbook.json --brief
python skills/campus-card-skill/scripts/card-audit.py examples/worldbook.json
```

The query should report `total_entries: 1` and the library entry (`图书馆`). The audit should report `format: "st-worldbook"`, an empty `errors` array, and entry statistics. Both commands leave the input unchanged and require only the Python standard library.

The included [worldbook JSON](examples/worldbook.json) is synthetic demonstration data, not a full character card or a verified platform import. After the sample works, substitute your own file path.

| Input | Tool |
| --- | --- |
| Standalone ST worldbook with an `entries` mapping | `query.py` for summaries, searches, and entry lookup |
| ST v2/v3 card, taberna wrapper, or standalone ST worldbook JSON | `card-audit.py` for read-only structural checks |
| PNG character card | Export JSON in your platform first; these tools do not extract PNG metadata |

## Install the skills

Copy **both complete directories** from `skills/` into your agent's skills directory. For a project using `.agents/skills/`, keep this layout:

```text
your-project/
└── .agents/skills/
    ├── campus-card-skill/
    │   ├── SKILL.md
    │   ├── references/
    │   └── scripts/
    └── world-book-skill/
        ├── SKILL.md
        └── scripts/
```

Keep the directories beside each other: the worldbook skill refers to the main skill's guides. Installing only `SKILL.md` loses required references. Use your agent's supported skills location if it differs, and verify that both skills are available in the intended project. CLI use does not require skill installation.

Then give the agent a file and a bounded task:

```text
Use $campus-card-skill to review ./card.json for inconsistent motivations
and a confusing opening scene. Explain the problems first. Change only the
parts I request and preserve unrelated fields and entry IDs.
```

Use `$world-book-skill` for the SillyTavern-oriented entry point. See the [Chinese reference table](README.md#参考指南) for detailed guides by task.

## Troubleshooting and scope

- **Missing skill references:** copy complete folders and keep both skills at the same level.
- **Empty query output from a card:** the query tool expects a standalone worldbook; use the audit tool for embedded card structures.
- **A clean audit but unexpected platform behavior:** test the platform import, activation rules, budget, and conversations separately. The audit does not simulate them or count model tokens.

The CLI tools read local JSON up to 8 MiB, do not make network requests, do not execute card content, and do not modify files. Query output can contain private creative material. When using an agent for writing, data handling depends on that agent and its model service. Read [SECURITY.md](SECURITY.md) for the complete scope.

## Feedback and contributions

[Report a problem](https://github.com/Marco0431/character-card-skills/issues/new?template=bug_report.md) with the platform, JSON format, Python version, exact command, expected result, and a small synthetic example. Remove private character details, conversations, and credentials before publishing attachments.

Useful contributions include reproducible compatibility cases, terminology corrections, and clearer writing guidance. For tool changes, run the existing checks:

```sh
python -m unittest discover -s skills/campus-card-skill/scripts -p "test_*.py"
python -m unittest discover -s tests -p "test_*.py"
```

The repository currently has no `LICENSE` file; it does not grant unrestricted redistribution or commercial-use permission. Contact the author about those uses. The [documentation index](llms.txt) links to the individual guides and scripts.
