# Restaurant - Reputation management

**Demo business:** Casa Olmo Trattoria (fictional)
**What the business buys:** Reputation management

Every new review gets a reply drafted for the owner; low ratings raise an alert straight away.

**What it replaces:** Reviews that stay unanswered for months.

## Flow

```mermaid
flowchart LR
  T[Webhook (new record arrives)] --> S[Sample data]
  M[Manual run] --> S
  S --> R[Rules]
  R --> Q{Needs action?}
  Q -- yes --> D[Draft message] --> A[Owner approval] --> X[Send] --> L[Log]
  Q -- no --> N[No action]
```

## Sample run

4 sample records: 3 produce a draft, 1 are skipped.

| Record | Result |
|---|---|
| R-01 | draft: positive review without a reply |
| R-02 | draft: negative review without a reply |
| R-03 | draft: positive review without a reply |
| R-04 | skipped: already answered |

Example draft (R-01):

> Dear Helen, thank you for the kind words. We are glad you enjoyed your visit and look forward to seeing you again.

Full output is in `sample-output.json`. Dates in the sample data are generated relative to today, so the result is the same whenever you run it.

## Files

- `workflow.json`: n8n workflow, import and press *Manual run*
- `sample-data.json`: the records used in the demo
- `sample-output.json`: what the run produces

## Skeleton, not production

The message is built from a template in a Code node, and approval and sending are placeholder nodes. Going live means swapping in the real data source, an LLM call, a send channel and an approval step.
