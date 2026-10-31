# Engagement Report — TEMPLATE (BLANK)

## 1. Executive summary

- Engagement: [name, dates]
- Scope summary: [systems, categories — no more than the signed scope]
- Overall assessment: [to be filled in after testing]
- Number of findings by severity: Critical __ High __ Medium __ Low __ Informational __

## 2. Scope and method

- Signed scope reference: [document, date]
- Test window actually used: [dates, times]
- Test accounts used: [account names only]
- Tools used: [name and version]
- Items explicitly NOT tested, and why: [to be filled in]

## 3. Findings

For each finding, use this structure and no other:

### Finding N: [title]

- Severity: [Critical / High / Medium / Low / Informational]
- Affected system: [in-scope system only]
- Category: [e.g. authentication, access control, configuration]
- Description: [what was observed, in neutral technical language]
- Evidence: [redacted logs, screenshots, or command output — no secrets,
  no personal data, no credentials]
- Impact if exploited: [realistic, scoped to this system]
- Reproduction steps (test account, lab or test environment only):
  1. [step]
  2. [step]
- What was NOT done: [e.g. no real user data accessed, no production
  modification, no lateral movement — state the limits honestly]
- Remediation: [concrete, testable fix]
- Owner response: [to be filled in by the owner]

## 4. Retest notes

- Findings retested: [list]
- Result per finding: [fixed / partially fixed / not fixed]
- Retest scope reference: [new scope document, if applicable]

## 5. Appendices

- A. Redacted evidence index
- B. Tool output index (redacted)
- C. Communication log (dates and topics, no message contents with secrets)
