# Evidence Handling

## Principles

1. Collect the minimum evidence that proves the finding — nothing more.
2. Redact before sharing: secrets, tokens, session identifiers, personal
   data, internal addresses, and credentials are removed from every
   artefact that leaves the engagement environment.
3. Evidence is stored in one place, encrypted at rest, with access limited
   to the engagement team.
4. Every artefact records its provenance: when it was collected, from
   which in-scope system, with which test account, and under which scope.

## What to collect per finding

- The request and response that demonstrate the issue (redacted).
- The system and version, if the owner has agreed to share it.
- The time of the observation, in the scope timezone.
- A note of what was deliberately not done (for example: "stopped before
  reading the returned record's contents").

## What never to collect

- Real user data, real credentials, real tokens, real personal data.
- Data from out-of-scope systems, even if it was returned by accident.
  If it is received, it is deleted, the incident is logged, and the owner
  is notified — it is not used as evidence.

## Retention and deletion

- Retention period: as agreed in the signed scope, and no longer.
- At the end of the period, engagement data is deleted and the deletion
  is confirmed to the owner in writing, with the date and the scope of
  what was deleted.
- If the owner requests earlier deletion, that request takes precedence.

## Reporting

Public or portfolio write-ups, if the owner agrees to any, contain only
redacted, owner-approved material, after the agreed remediation window.
A finding is never published with enough detail to reproduce it against
a system that has not yet been fixed, unless the owner has explicitly
agreed to that publication.
