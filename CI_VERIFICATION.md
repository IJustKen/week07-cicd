# CI verification

Fill this in after you push and watch the workflow run on GitHub (Actions
tab of your repo). This is how we confirm your CI actually ran green in a
real GitHub Actions runner, not just locally.

## Workflow run

Paste the URL of a successful run of all three jobs (Actions tab -> click
the run -> copy the URL):

https://github.com/IJustKen/week07-cicd/actions/runs/35903626968

## Job summary

For each job, note pass/fail and how long it took:

- `lint`: succeeded 2 minutes ago in 10s
- `unit-test`: succeeded 2 minutes ago in 7s
- `integration-test`: 1 minute ago in 20s

## What broke on the way there (optional but useful)

If any job failed before you got it working, briefly note what the failure
was and what fixed it. (Not required, but if `integration-test` gave you
trouble, this is worth 2 sentences for your own future reference — Week 9's
lab also builds on debugging CI-style failures.)

**Path duplication error in ci.yml**: Setting defaults.run.working-directory: ./week07-cicd caused GitHub Actions to look inside a nested /week07-cicd/week07-cicd path, failing the pipeline during dependency installation. Removing the working-directory attribute resolved the path conflict. This was a mistake from my end as I copy pasted the version I made for the other repo.
