# Sources and fold-in provenance

This skill is an original synthesis tailored to a real-life manager use case. It does not vendor full third-party skill text.

## openclaw-personal-assistant
- Repository: https://github.com/markus-lassfolk/openclaw-personal-assistant
- Relevant file: `skills/personal-assistant/SKILL.md`
- Concepts folded in:
  - maintain a live operational picture/control tower
  - detect overdue and looming deadlines
  - prepare the next best action proactively
  - reconcile inbox/calendar/tasks/memory/project state
  - distinguish internal preparation from consequential external actions
- License status observed during fold-in: no root `LICENSE` file was found, so this repository uses only high-level concepts and original wording rather than vendoring substantial source text.

## agentic-life-os
- Repository: https://github.com/djangonavarro220/agentic-life-os
- Relevant file: `skills/life-os/SKILL.md`
- Concepts folded in:
  - current-context / next-action orientation
  - dynamic low-noise heartbeat rather than a fixed noisy checklist
  - source-of-truth pointers instead of duplicating all personal data
  - load only the capabilities relevant to the current intent
  - silence is valid when nothing actionable changed
- License: MIT.

## corpus-to-skill
- Repository: https://github.com/nicholasswhite/corpus-to-skill
- Relevant file: `SKILL.md`
- Concept folded in:
  - explicit Update / Fold-in workflow for improving an existing skill from new material
- License: MIT.

## Local meta-skill
Future source additions to this skill should use:
`../skill-integrator/SKILL.md`

For every future fold-in, record source, path/ref, license status, capabilities added/upgraded/rejected, and date.
