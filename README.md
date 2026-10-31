# RedTeam-Engagement-Kit

A methodology kit for authorised penetration testing and red-team engagements.
It contains templates, checklists and process guides only. It contains no
exploit code, no payloads, and no tooling for attacking any system.

## What this is for

An engagement that can be shown to a reviewer, a client, or an oversight
body: written scope, written authorisation, a named human in charge, stop
conditions, evidence handling, and a report format. The technical skill of
finding a weakness is only half of a red-team engagement; the other half is
proving that the work was authorised, bounded, and reversible.

## What this is NOT for

- Testing any system without prior written authorisation.
- Testing production systems, third-party systems, or systems belonging to
  someone else.
- Phishing real users, social engineering real staff, or exfiltrating real
  data. Templates in this repository are blank for a reason: they are filled
  in only for a real, authorised engagement, and never with invented clients.

## Contents

- `docs/rules-of-engagement.md` — the rules that govern every engagement.
- `templates/scope-authorisation.md` — scope and authorisation, to be signed
  before any testing starts.
- `templates/pre-engagement-checklist.md` — checks that must pass before day 1.
- `templates/report.md` — blank report structure.
- `templates/legal-attestation.md` — blank, unsigned attestation template.
- `guides/evidence-handling.md` — how findings and evidence are stored.
- `guides/human-oversight-stop-conditions.md` — who may stop the work, and when.
- `guides/risk-register.md` — how engagement risk is recorded and reviewed.

## Rule of the kit

If it is not in the signed scope, it is out of scope. If the authorisation
cannot be produced, the engagement does not start. If a stop condition is
met, testing stops first and the discussion happens afterwards.
