# week07-cicd

## Configured the GitHub Actions Pipeline (.github/workflows/ci.yml)
I built a multi-job workflow with a Directed Acyclic Graph (DAG) dependency structure:

lint job: Runs flake8 src/ on Python 3.11 to enforce code style.

unit-test job: Runs pytest tests/ on Python 3.11 to test API endpoints in-memory without Docker.

integration-test job: Declares needs: [lint, unit-test]. It makes scripts/integration_test.sh executable (chmod +x) and runs it to test the full container lifecycle.

## Created the Integration Test Script (scripts/integration_test.sh)
I wrote a Bash script to verify the containerized application end-to-end:

Built the Docker image from the root Dockerfile (docker build -t week7-detector .).

Ran the container in detached mode mapped to port 8080 (docker run -d -p 8080:8080 --name week7-detector-ci --rm week7-detector).

Polled the /health endpoint until the server started responding (curl -sf http://localhost:8080/health).

Tested the /detect endpoint by sending a POST request with a sample image fixture (curl -sf -F "image=@data/fixtures/camera_A_daylight/000.jpg" http://localhost:8080/detect).

Verified that the JSON response contained "detections".

Cleaned up the container automatically on script exit using a trap cleanup EXIT hook.



## Verification & Documentation
Tested scripts locally before pushing to ensure permissions and syntax were correct.

Pushed changes to GitHub to trigger the Actions runner and verified all three jobs went green.

Generated and documented the successful workflow run URL in CI_VERIFICATION.md.