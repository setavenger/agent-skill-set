# agent-skill-set

Shared Cursor skills library for agent-assisted development. Skills live under `.cursor/skills/` and are copied or synced into application repos that need them.

This repo has **no application UI of its own** — it is a distribution hub, not a product codebase.

## Skill categories

| Category | Skills | When to use |
|----------|--------|-------------|
| **SwiftUI & layout** | `swiftui-patterns`, `swiftui-navigation`, `swiftui-layout-components`, `swiftui-performance` | Structuring SwiftUI apps, navigation, lists/forms, performance audits |
| **Swift platform** | `swift-language`, `swift-concurrency`, `swift-charts`, `core-data`, `ios-networking` | Language idioms, concurrency, charts, persistence, networking |
| **Apple frameworks** | `healthkit`, `mapkit`, `push-notifications`, `permissionkit`, `storekit`, `background-processing` | Health, maps, notifications, IAP, background tasks |
| **Agent workflow** | `subagent-orchestration`, `linear`, `domain-modeling` | Orchestration, issue tracking, domain language & ADRs |
| **Communication** | `caveman`, `ponytail`, `grilling`, `grill-with-docs` | Token-efficient replies, minimal solutions, plan stress-testing |
| **UI/UX (optional)** | `ui-ux-pro-max` | See below — vendor into repos doing UI/UX work |

## ui-ux-pro-max (optional vendoring)

`ui-ux-pro-max` is a searchable design guide (styles, palettes, typography, UX rules, stack-specific patterns). It is **optional** and **not required** for:

- Pure iOS/Swift engineering (use SwiftUI skills + the app's `DESIGN_GUIDELINES` instead)
- Backend-only or skills-only repos like this library

**Vendor it when** a consumer repo is doing meaningful UI/UX work — especially **greenfield web** (Next.js, HTML/Tailwind, shadcn). Copy the whole folder:

```bash
cp -r /path/to/agent-skill-set/.cursor/skills/ui-ux-pro-max .cursor/skills/
```

Or refresh from upstream:

```bash
npx --yes ui-ux-pro-max-cli init --ai cursor
```

**In consumer repos:**

1. Set the target stack in skill usage (`--stack nextjs`, `html-tailwind`, `shadcn`, `react-native`, `swiftui`, etc.) — the hub copy is stack-agnostic.
2. Keep the product's **`DESIGN_GUIDELINES`** (or equivalent) as the **authority** over this skill. For example, RunRecords uses its own design doc; `ui-ux-pro-max` is supplementary at most.
3. Do not add this skill to repos that will never ship UI.

## Adding skills to a consumer repo

1. Copy `.cursor/skills/<skill-name>/` into the target repo's `.cursor/skills/`.
2. Commit the skill files so agents in that repo can discover them.
3. Reference repo-specific rules in the consumer's `AGENTS.md` or `.cursor/rules/` as needed.
