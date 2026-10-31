# Rules of Engagement

These rules apply to every engagement run under this kit. They are
deliberately strict: a rule that can be waived casually is not a rule.

## 1. Written authorisation first

No testing begins until a scope document is signed by a person with
authority over the target systems. A chat message, a verbal assurance, or
a forwarded email thread is not authorisation. The signed document names:

- the organisation and the authorising person (name, role);
- the systems in scope, by name and address;
- the systems explicitly out of scope;
- the test window (dates and times, including timezone);
- the permitted test categories (for example: network, web application,
  configuration review — not "everything");
- the contact for escalation and for emergency stop.

## 2. Scope is a boundary, not a suggestion

- Anything not listed as in scope is out of scope.
- A discovery that a neighbouring system looks interesting does not expand
  scope. It is recorded as an observation and reported to the owner, who
  decides whether to authorise a follow-up.
- Shared infrastructure, third-party services, and production data stores
  are out of scope unless named explicitly, which they normally are not.

## 3. No real data, no real harm

- Test accounts are used wherever they exist. Real user accounts are never
  used, and real user data is never read, copied, or exfiltrated.
- Destructive actions (deletion, modification of production data,
  denial-of-service testing, ransomware simulation against real data) are
  prohibited unless explicitly authorised in writing, with a tested
  rollback plan. The default is: prohibited.
- Rate limits in the scope are respected. "The limit was not enforced" is
  a finding to report, not permission to exceed it further.

## 4. Human oversight

A named human tester is responsible for every action taken. Automated
tooling may assist discovery, but:

- every action that changes state, authenticates, or sends data requires
  a human decision for that case;
- the tester reviews tool output before acting on it;
- the tester can stop the engagement at any time, without approval.

## 5. Stop conditions

Testing stops immediately, and the owner is notified, if any of the
following occurs (full list in `guides/human-oversight-stop-conditions.md`):

- an out-of-scope system is affected;
- a production service degrades or becomes unavailable;
- real personal data is encountered;
- the authorisation is withdrawn or its window expires;
- the tester is unsure whether an action is authorised.

Work resumes only after the owner confirms in writing that it may.

## 6. Evidence and reporting

- Every finding records: what was tested, when, with what account and
  scope, what was observed, and what was NOT done.
- Screenshots and logs are redacted before they leave the engagement
  environment. Secrets, tokens and personal data are never included.
- The report distinguishes confirmed findings, suspected findings that
  could not be confirmed within scope, and items that were not tested.

## 7. After the engagement

- Test accounts and access granted for the engagement are revoked or
  confirmed revoked by the owner.
- Engagement data is retained only for the period agreed in the scope,
  then deleted, and the deletion is confirmed to the owner.
- A retest, if agreed, is a new engagement with its own scope, not an
  extension of the old one.
