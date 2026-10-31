# Human Oversight and Stop Conditions

## The human in charge

Every engagement has one named engagement lead. That person:

- approves the test plan for the day;
- reviews automated tool output before any action is taken on it;
- is the only person who may authorise a state-changing action;
- may stop the engagement at any time, for any reason, without seeking
  permission first.

If the lead is unavailable, testing pauses. It does not continue under
an acting lead who has not been briefed on the scope.

## Automation boundaries

Automated tooling may:

- enumerate in-scope endpoints and parameters;
- run read-only checks that the scope permits;
- draft findings for human review.

Automated tooling may not, without a human decision for that specific
case:

- authenticate as any account;
- submit, modify, or delete data;
- follow a redirect or a reference to a system outside the scope;
- send messages to any user, real or test.

## Stop conditions — stop first, discuss afterwards

Stop testing immediately and notify the owner if:

1. An out-of-scope system is affected, or an action touches one.
2. A production service degrades, errors, or becomes unavailable.
3. Real personal data, real credentials, or real tokens are encountered.
4. The authorisation window expires, or authorisation is withdrawn.
5. A test account behaves as a real user account, or vice versa.
6. The tester is unsure whether an action is authorised.
7. A tool behaves unexpectedly (for example: it follows links outside
   the target, or it retries aggressively).
8. The owner asks for a stop, for any reason.

## Resuming

Work resumes only when:

- the cause is understood and recorded;
- the owner confirms in writing that testing may resume, and under what
  changed conditions, if any;
- the scope document is updated if the conditions changed, and re-signed
  if the change is material.

A stop is not a failure of the engagement. It is the control working.
