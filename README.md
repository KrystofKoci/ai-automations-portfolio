# 7 businesses, 7 automations

Seven small n8n workflow skeletons, one per type of local business. Each one answers a single question: *what is the one thing this business would pay to have done automatically?*

All seven share the same skeleton: **trigger → data → rules → draft → approval → send → log**. Only the data and the rules change.

| Automation | What the business buys | Trigger | Sample records | Drafts produced |
|---|---|---|---|---|
| [Law firm - Speed to lead](01-law-firm-speed-to-lead/) | Speed | webhook | 4 | 3 |
| [Gym - Membership retention](02-gym-membership-retention/) | Membership retention | schedule | 5 | 3 |
| [Restaurant - Reputation management](03-restaurant-reputation/) | Reputation management | webhook | 4 | 3 |
| [Real estate - Lead follow-up](04-real-estate-follow-up/) | Follow-up | schedule | 5 | 3 |
| [Med spa - Full calendar](05-med-spa-full-calendar/) | Full calendars | schedule | 3 | 2 |
| [Dentist - Checkup recall](06-dentist-checkup-recall/) | Booked checkups | schedule | 5 | 2 |
| [HVAC - Automated follow-ups](07-hvac-automated-follow-up/) | Automated follow-ups | schedule | 5 | 2 |

## Try it

1. In n8n choose **Import from file** and pick any `workflow.json`.
2. Press **Manual run**. Sample data is built in, no credentials are needed.
3. Open the *Draft message* and *Log* nodes to see the result.

## Design choices

- **Rules before AI.** Who gets contacted is decided by plain, testable rules. The model only writes the wording.
- **Human in the loop.** Each draft carries an `approval` field: routine messages can go out on their own, anything sensitive waits for the owner.
- **Honest about automation.** Every draft says it was prepared by an automated assistant.
- **Consent first.** Records without permission to be contacted are skipped (see the med spa and dentist examples).

## Status

Portfolio demo. Business names, people and data are fictional. Messages come from templates, sending and approval are placeholders.
