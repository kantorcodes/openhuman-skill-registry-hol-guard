# OpenHuman Skill Registry

Community index of installable [Agent Skills](https://agentskills.io) for [OpenHuman](https://github.com/tinyhumansai/openhuman).

## How it works

OpenHuman's skill browser fetches `index.json` from this repo to populate the catalog. Each entry points to a `SKILL.md` file that follows the [Agent Skills specification](https://agentskills.io/specification).

## Adding a skill

1. Create a directory under `skills/` with your skill slug (lowercase, hyphens only).
2. Add a `SKILL.md` following the [agentskills.io spec](https://agentskills.io/specification).
3. Add an entry to `index.json` with the `download_url` pointing to the raw GitHub URL.
4. Open a PR.

## Index format

```json
{
  "skills": [
    {
      "id": "my-skill",
      "name": "My Skill",
      "description": "What it does and when to use it.",
      "format": "agentskills",
      "author": "your-name",
      "version": "1.0.0",
      "tags": ["tag1", "tag2"],
      "download_url": "https://raw.githubusercontent.com/tinyhumansai/skill-registry/main/skills/my-skill/SKILL.md"
    }
  ]
}
```
