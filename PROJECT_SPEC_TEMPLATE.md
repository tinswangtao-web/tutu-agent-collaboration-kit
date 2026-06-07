# PROJECT_SPEC

> Copy this file into a project repo as `PROJECT_SPEC.md` after Brainstorm / Architect Discovery Mode.
> This file defines product intent only. Do not put implementation details, code plans, command logs, or handoff notes here.

## One Sentence Goal

- <One sentence describing what the product helps the target user accomplish.>

## Target User

- Primary user: <one primary user group only>

## User Workflow

Use real user actions. Do not discuss technical implementation.

```text
Open
→ <operate>
→ <save / submit>
→ <view result>
```

## UI / UX Scope

For user-facing products, define the experience before UI implementation. Do not discuss technical implementation.

- Primary screens / views:
- Main workflow start:
- Main workflow end:
- Required user actions per screen:
- Essential states:
  - empty:
  - loading:
  - error:
  - saved / success:
  - result view:
- Navigation / page flow:
- Visual direction or design constraints:
- UI milestone: Current Milestone / Next Milestone / Not Now

## MVP

The smallest runnable useful version MUST include:

- <MVP item 1>
- <MVP item 2>
- <MVP item 3>

## Not Now

Explicitly out of scope for the current milestone:

- <feature / module / optimization not allowed now>
- <feature / module / optimization not allowed now>

## Current Milestone

- <current product milestone>

## Next Milestone

- <the single next milestone Architect may turn into Builder Task Cards>

## Spec Update Rule

- Architect owns this file.
- Brainstorm / Discovery Mode produces or updates this file.
- Architect must run Spec Quality Gate before Execution Mode.
- User must confirm new projects, new modules, large features, and major direction changes before Builder Task Cards are generated.
- Builder does not reinterpret, expand, or modify this file unless an Architect Task Card explicitly asks for a spec file update.
- `AI_CONTEXT.md` may summarize current Product State, but this file remains the product spec source of truth.
