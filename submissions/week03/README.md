# Week 3 Submission - Individual Readiness Lab

## Student information

- Name: PAN, Wei
- Student ID: 21315290
- Repository: https://github.com/powerpan/MAIE6000C-starter-eric
- Checkpoint tag: `w03-readiness`
- Commit SHA: Resolve from `w03-readiness^{commit}` after the tag is created

## 1. What I changed

I added `mfa` to the access-request keywords used by the internal triage
service. A request that only mentions an MFA problem is now classified as an
access issue instead of falling back to the general category.

I also added a focused regression test for this case. To make the same checks
available inside the project container, the Docker image now installs the
development dependencies and includes the test directory.

## 2. Files touched

- `services/ai/app/main.py`
- `tests/unit/test_ai_service.py`
- `Dockerfile`

## 3. How I verified it

- Ran Ruff against the repository; it completed without errors.
- Ran the unit and integration tests; all 5 tests passed.
- Ran the full test suite; 5 tests passed and 1 smoke test was skipped as
  expected when no smoke-test URL was supplied.
- Ran the smoke test against the Compose stack; the test passed.
- Sent an MFA-only request to `/triage`; the response used the `access` label
  with a confidence score of `0.63`.
- Confirmed that the GitHub Actions `test` job passed for the pull request.

## 4. Known limitations or notes

The triage service is still a small keyword-based classifier. This change only
adds the missing MFA term; it does not add contextual classification or change
the existing category order.
