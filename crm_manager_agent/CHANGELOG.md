# Changelog

All notable changes to the NowcastIQ Agent are documented here.
Format: [version] — date — description

---

## [1.0.0] — 2026-03-16 — Initial release

**Built & validated:**
- All 5 Attio lists covered: 1.0, B1, 2.0, 3.0, 3.1
- Task creation for all lead types with correct owners and priorities
- Trial health discrepancy flagging (read-only, never writes)
- Trial outcome flagging (deal stage vs stored result)
- Out-of-criteria detection with one-time flag + override persistence
- Day-5 and day-10 task escalation (no duplicate task sprawl)
- Daily completion digest task in Attio
- Structured JSON run logs with rolling 14-run pilot summary
- Rollback: every created task logged, `--rollback <run-id>` to undo
- Health check: `--health` flag verifies all APIs and lists
- Claude API credit tracking with per-run token and cost report
- Error isolation: per-list catch blocks, fatal error tasks in Attio

**Validated live against Attio:**
- All field slugs confirmed (trial_health_6, trial_result_3, activation_stage, stage, segment, lead_status)
- Task creation + completion confirmed
- Task query param (`linked_record_object`) confirmed
- getAttrValue tested 8/8 against real REST API response format
- Date logic tested against real DRW trial (correct trigger behaviour confirmed)

---

## How to add a new version entry

When you make a change to the agent code:

1. Update `VERSION` constant at the top of `nowcastiq-agent.mjs`
2. Update `version` field in `package.json`
3. Add an entry here in the format:

```
## [X.Y.Z] — YYYY-MM-DD — Short title

**Changed:**
- What was changed and why

**Fixed:**
- What bug was fixed

**Added:**
- What new feature was added
```

4. Commit: `git add -A && git commit -m "vX.Y.Z: short description"`

---

## Versioning rules

- **Patch** (1.0.X): Bug fixes, rule threshold tweaks, task description updates
- **Minor** (1.X.0): New task types, new list support, new flags added
- **Major** (X.0.0): Breaking changes to Attio field slugs, list restructure, architecture change
