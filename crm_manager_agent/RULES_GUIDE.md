# Agent Rules Guide

The agent reads `rules.json` on every run. You can change any rule below without touching `nowcastiq-agent.mjs`. The change takes effect on the next run automatically.

---

## How to Change a Rule

1. Open `rules.json` in any text editor
2. Find the rule you want to change
3. Edit the value
4. Save the file
5. Next agent run picks it up automatically — no restart needed

Or tell me what you want changed in chat and I'll update the file for you.

---

## What You Can Change

### Trial Rules (`trials.*`)

| Rule | Field | What it does | Default |
|------|-------|-------------|---------|
| Call for Demo | `callForDemo.triggerWithinDays` | How many days after trial start to trigger call | `3` |
| Call for Demo | `callForDemo.owner` | Who gets the task | `diana` |
| Mid-Point Check | `midPointCheck.triggerOnDayMin/Max` | Which day range triggers the check | `6–8` |
| Mid-Point Check | `midPointCheck.owner` | Who gets the task | `naseef` |
| Feedback & Pricing | `feedbackAndPricing.triggerDaysBeforeEnd` | Days before trial end to trigger | `3` |
| Final Check-in | `finalCheckIn.triggerDaysBeforeEnd` | Days before trial end to trigger | `2` |
| Escalation | `escalation.staleTaskDays` | Days with no response before task gets urgency flag | `5` |
| Escalation | `escalation.considerClosingDays` | Days with no response before "consider closing" note | `10` |

### Deal Rules (`deals.*`)

| Rule | Field | What it does | Default |
|------|-------|-------------|---------|
| Closing Soon | `closingSoon.triggerWithinDays` | Alert when deal closes within X days | `7` |
| Procurement default due | `trackProcurement.defaultDueDays` | Days until due if no close date set | `7` |
| Expansion default due | `trackExpansion.defaultDueDays` | Days until due if no close date set | `14` |

### Universal Rules (`universal.*`)

| Rule | Field | What it does | Default |
|------|-------|-------------|---------|
| No team activity | `noTeamActivityDays` | Trigger re-engage task after X days silence | `14` |

---

## What You Can Disable

Set `"enabled": false` on any rule to stop the agent from creating that task type entirely.

Example — disable Mid-Point Checks:
```json
"midPointCheck": {
  "enabled": false,
  ...
}
```

---

## What You Can't Change in rules.json

These are hardcoded for safety or business logic reasons:

- **List B1 newsletter tasks always go to Naseef** — this is a hard rule, not configurable
- **Trial health is always read-only** — agent never writes `trial_health_6`
- **Lifecycle stage is always read-only** — agent never modifies lifecycle

To change these, the code in `nowcastiq-agent.mjs` needs to be updated. Tell me what you want and I'll make the change.

---

## Examples

**"Move the demo call deadline to within 2 days, not 3"**
```json
"callForDemo": {
  "triggerWithinDays": 2,
  ...
}
```

**"Give the Feedback & Pricing task to Naseef instead of Diana"**
```json
"feedbackAndPricing": {
  "owner": "naseef",
  ...
}
```

**"Escalate stale tasks after 7 days instead of 5"**
```json
"escalation": {
  "staleTaskDays": 7,
  "considerClosingDays": 14,
  ...
}
```

**"Stop creating Mid-Point Check tasks"**
```json
"midPointCheck": {
  "enabled": false,
  ...
}
```

---

## Valid Values

- **owner**: `"naseef"`, `"diana"`, or `"ed"`
- **priority**: `"URGENT"`, `"HIGH"`, `"MEDIUM"`, `"LOW"`
- **enabled**: `true` or `false`
- **days fields**: any positive integer
