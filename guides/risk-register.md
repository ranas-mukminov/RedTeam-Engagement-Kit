# Risk Register

Record engagement risks before testing starts, review them daily during
the engagement, and close them at the end. This is a working document,
not a formality: a risk that is not written down is not managed.

## Register format

| ID | Risk | Likelihood | Impact | Mitigation | Owner | Status |
|---|---|---|---|---|---|---|
| R-01 | Example: test action affects production availability | Low | High | Test only in the agreed window; stop on first error; owner contact on standby | Engagement lead | Open |
| R-02 | [to be filled in] | | | | | |

## Risks that must always be considered

1. **Scope creep** — Mitigation: daily scope check against the signed
   document; any new system is an observation, not a target.
2. **Production impact** — Mitigation: agreed window and blackout
   periods; rate limits respected; stop on degradation.
3. **Real data exposure** — Mitigation: test accounts only; stop and
   notify if real data is encountered; redact all evidence.
4. **Credential exposure** — Mitigation: no production credentials held;
   test credentials stored separately and rotated after the engagement.
5. **Third-party impact** — Mitigation: third-party services are out of
   scope by default; findings involving them are reported to the owner,
   not tested further.
6. **Tool misbehaviour** — Mitigation: tools reviewed before use;
   human approval for state-changing actions; stop on unexpected behaviour.
7. **Report leakage** — Mitigation: reports are confidential engagement
   material; distribution is limited to the owner and agreed recipients.

## Review

- Before day 1: full register reviewed by the engagement lead.
- Daily during testing: new risks added, mitigations checked.
- At close: every risk marked closed or transferred to the owner, with
  the reason recorded.
