# NOTES.md — Week 7: CI/CD Integration Testing

**Student ID used with `generate_for_student.py`:**
142301038


## Why gate integration-test on needs: [lint, unit-test]?

<!-- Why does integration-test need needs: [lint, unit-test] instead of
     just running in parallel with them — what's the actual cost being
     avoided? -->
     
Gating integration-test behind needs: [lint, unit-test] saves both time and CI compute costs.

Linting and unit tests take less than 10 seconds to run. Building and booting up a full Docker container for an integration test takes much longer and uses way more resources.

If someone makes a simple typo or breaks a unit test, there’s no point wasting runner minutes building a container for code that's already broken. Running fast checks first gives instant feedback and prevents unnecessary container builds.