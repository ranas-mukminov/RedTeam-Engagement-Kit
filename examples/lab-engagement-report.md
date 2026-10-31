# Engagement Report — LAB ENGAGEMENT (NOT A CLIENT ENGAGEMENT)

**Read this first:** this report is a worked example of the kit's
own process, run against the author's own lab repositories only.
There is no client, no vendor, and no production system here. The
findings below are the known, intentionally planted flaws in those
labs, reproduced and then verified fixed. Nothing in this report
is a real-world disclosure, and no real user data was involved.

## 1. Executive summary

- Engagement: LAB-2026-001, lab run on 2026-10-31
- Scope summary: VulnLab-App and API-Red-Lab (local lab code and
  localhost servers only). Out of scope: everything else, including
  any production system, third-party service, and real user data.
- Overall assessment: the labs behaved as designed — every planted
  flaw reproduced in its vulnerable form and was blocked in its
  fixed form. The fixed forms are the remediation for each finding.
- Findings by severity: High 5, Medium 3, Low 1, Informational 0
  (counts are for lab findings only; see section 3).

## 2. Scope and method

- Signed scope reference: none — a lab engagement needs no client
  scope document, because there is no client. The scope is stated
  in this section and nowhere else.
- Test window actually used: a single local lab session, 2026-10-31.
- Test accounts used: fictional lab accounts only
  (`lab-alice`, `lab-bob`); no real accounts.
- Tools used: the labs' own unit-test suites and their localhost
  HTTP servers (VulnLab-App on 127.0.0.1, API-Red-Lab on 127.0.0.1),
  plus curl over localhost. No external scanning tool, no
  production probe.
- Items explicitly NOT tested, and why: production systems (not
  in scope, not owned for testing here), third-party APIs (not in
  scope), real user data (never used in a lab).

## 3. Findings

### Finding 1: SQL injection in lab search (VulnLab-App)

- Severity: High (lab severity; the flaw class is high in real systems)
- Affected system: VulnLab-App, lab search function only
- Category: injection
- Description: the vulnerable search builds a query from user input,
  so a crafted lab input returns every fictional user.
- Evidence: unit test `test_vuln_returns_all_on_injection` (3 rows
  returned); fixed version returns 0 rows for the same input.
- Impact if exploited: in a real system, unauthorised data read.
  In this lab, only fictional records exist.
- Reproduction steps (lab only):
  1. Run the VulnLab-App test suite, or query the localhost server
     `/search` with the lab injection input from the exercises.
  2. Observe all fictional users returned in vulnerable mode.
- What was NOT done: no real database, no real data, no external host.
- Remediation: parameterised queries, as in `lab/fixed.py`.
  Retest: fixed search returns 0 rows for the injection input.

### Finding 2: Reflected XSS in lab greeting (VulnLab-App)

- Severity: Medium (lab)
- Affected system: VulnLab-App, lab greeting renderer only
- Category: cross-site scripting
- Description: user input is rendered unescaped in vulnerable mode.
- Evidence: unit test showing a script tag rendered raw in
  vulnerable mode and escaped in fixed mode.
- Impact if exploited: in a real system, script execution in a
  victim browser. In this lab, no browser victim exists.
- Reproduction steps (lab only): query the localhost `/greet`
  endpoint with a script-tag lab input; compare vulnerable and
  fixed output.
- What was NOT done: no real browser, no real user session.
- Remediation: escape user input at render time, as in `lab/fixed.py`.

### Finding 3: IDOR — another user's lab record (VulnLab-App)

- Severity: High (lab)
- Affected system: VulnLab-App, lab record accessor only
- Category: access control
- Description: the vulnerable accessor performs no ownership check.
- Evidence: `lab-alice` reads `lab-bob`'s fictional record in
  vulnerable mode; fixed mode raises PermissionError (403 over HTTP).
- Impact if exploited: in a real system, unauthorised access to
  another user's data. In this lab, only fictional records exist.
- Reproduction steps (lab only): query `/record?owner=lab-bob&caller=lab-alice`.
- What was NOT done: no real user data accessed.
- Remediation: server-side ownership check per object, per request.

### Finding 4: SSRF validation missing (VulnLab-App, simulated)

- Severity: High (lab, simulated)
- Affected system: VulnLab-App, lab URL fetcher only
- Category: server-side request forgery
- Description: the vulnerable fetcher accepts any URL, including
  internal hosts. The lab makes no real network request — the
  vulnerable version returns a canned string — so this finding
  demonstrates missing validation, not a real internal fetch.
- Evidence: unit tests for internal-host acceptance (vulnerable)
  and allowlist rejection (fixed, 400 over HTTP).
- Impact if exploited: in a real system, internal service access.
  In this lab, no internal service is reached.
- Reproduction steps (lab only): query `/fetch` with an internal
  lab URL; compare vulnerable and fixed responses.
- What was NOT done: no real network request, no metadata service.
- Remediation: allowlist outbound hosts, reject internal and
  metadata hosts, as in `lab/fixed.py`.

### Finding 5: Broken authentication — role claim trusted (VulnLab-App)

- Severity: High (lab)
- Affected system: VulnLab-App, lab admin gate only
- Category: authentication
- Description: a client-supplied role claim opens the admin panel
  in vulnerable mode.
- Evidence: unit tests showing the claim accepted in vulnerable
  mode and rejected in fixed mode without an issued token.
- Impact if exploited: in a real system, unauthorised admin access.
- Reproduction steps (lab only): query `/admin?role=admin` in
  vulnerable mode; query with an issued token in fixed mode.
- What was NOT done: no real admin account, no real session.
- Remediation: decide access from an issued session, never from
  a client-asserted role.

### Finding 6: BOLA — another user's API object (API-Red-Lab)

- Severity: High (lab)
- Affected system: API-Red-Lab, lab object accessor only
- Category: access control (OWASP API: Broken Object Level Authorisation)
- Description: the vulnerable accessor performs no ownership check.
- Evidence: unit tests and an HTTP smoke test (200 in vulnerable
  mode, 403 in fixed mode for the same request).
- Impact if exploited: in a real system, unauthorised object access.
- Reproduction steps (lab only): GET `/objects/obj-2?caller=lab-alice`.
- What was NOT done: no real API, no real user data.
- Remediation: server-side ownership check, as in `api/fixed.py`.

### Finding 7: Broken authentication — guessed token shape (API-Red-Lab)

- Severity: Medium (lab)
- Affected system: API-Red-Lab, lab authenticator only
- Category: authentication
- Description: the vulnerable authenticator accepts any token with
  the right shape, even if no session was issued.
- Evidence: unit tests and HTTP smoke tests (200 for a guessed
  shape in vulnerable mode, 401 for an unissued token in fixed mode).
- Impact if exploited: in a real system, account takeover by
  token guessing.
- Reproduction steps (lab only): GET `/auth?token=token-lab-alice`
  in vulnerable mode; GET with an unissued token in fixed mode.
- What was NOT done: no real session store, no real account.
- Remediation: accept only tokens present in the issued session
  table; in a real system, use random, expiring sessions.

### Finding 8: Excessive data exposure (API-Red-Lab)

- Severity: Medium (lab)
- Affected system: API-Red-Lab, lab profile endpoint only
- Category: data exposure
- Description: the vulnerable profile returns the whole record,
  including internal fields, to any caller.
- Evidence: unit tests showing internal fields present in
  vulnerable mode and absent (public fields only) in fixed mode.
- Impact if exploited: in a real system, internal data leakage.
- Reproduction steps (lab only): GET `/profile/lab-bob?caller=lab-alice`.
- What was NOT done: no real personal data involved.
- Remediation: filter at the API boundary to public fields only.

### Finding 9: No rate limiting (API-Red-Lab)

- Severity: Low (lab)
- Affected system: API-Red-Lab, lab rate limiter only
- Category: availability
- Description: the vulnerable limiter allows unlimited requests.
- Evidence: unit tests and HTTP smoke tests (fixed mode returns
  429 on the 4th and 5th requests in a row; vulnerable mode
  returns 200 throughout).
- Impact if exploited: in a real system, denial of service or
  credential-stuffing headroom.
- Reproduction steps (lab only): repeat GET `/rate?caller=lab-alice`.
- What was NOT done: no real traffic, no real service affected.
- Remediation: a per-caller budget with a 429 response, as in
  `api/fixed.py`.

## 4. Retest notes

- Findings retested: all 9, against the fixed implementations.
- Result per finding: fixed — every fixed version blocks the lab
  input that the vulnerable version accepted (see the evidence
  under each finding).
- Retest evidence: VulnLab-App unit suite 14 tests OK; API-Red-Lab
  unit suite 15 tests OK (including 4 HTTP smoke tests over
  127.0.0.1). These counts are from the local lab runs that
  produced this report, not from any production system.
- Retest scope reference: same lab scope as section 2; no new
  scope document, because there is no client.

## 5. Appendices

- A. Redacted evidence index: none needed — all evidence is lab
  data (fictional accounts, fictional records) and is already in
  the labs' test suites.
- B. Tool output index: VulnLab-App and API-Red-Lab test output
  (local runs, 2026-10-31).
- C. Communication log: not applicable — no client communication
  in a lab engagement.
