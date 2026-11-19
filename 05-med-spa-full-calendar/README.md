# Med spa - Full calendar

**Demo business:** Lumen Skin Studio (fictional)
**What the business buys:** Full calendars

Looks at open slots for the coming days and offers each one to the best-fitting client from the waitlist or lapsed list.

**What it replaces:** Empty chairs on Tuesday afternoon.

## Flow

```mermaid
flowchart LR
  T[Schedule (every morning)] --> S[Sample data]
  M[Manual run] --> S
  S --> R[Rules]
  R --> Q{Needs action?}
  Q -- yes --> D[Draft message] --> A[Owner approval] --> X[Send] --> L[Log]
  Q -- no --> N[No action]
```

## Sample run

3 open slots matched against 5 clients: 2 produce a draft, 1 are skipped.

| Record | Result |
|---|---|
| S-1 | draft: waitlist match |
| S-2 | draft: lapsed 120 days |
| S-3 | skipped: no consenting client for this treatment |

Example draft (S-1):

> Hi Elena, a facial appointment has opened at Lumen on 2026-11-20 at 14:00. Reply YES to take it and we will confirm. This message was prepared by an automated assistant. Reply STOP to opt out.

Full output is in `sample-output.json`. Dates in the sample data are generated relative to today, so the result is the same whenever you run it.

## Files

- `workflow.json`: n8n workflow, import and press *Manual run*
- `sample-data.json`: the records used in the demo
- `sample-output.json`: what the run produces

## Skeleton, not production

The message is built from a template in a Code node, and approval and sending are placeholder nodes. Going live means swapping in the real data source, an LLM call, a send channel and an approval step.
