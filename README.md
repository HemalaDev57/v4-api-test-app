# v4-api-test-app

A minimal Node.js Express app used to validate the CloudBees Platform v4 Runs and Run Details public APIs end-to-end.

This repo covers all 5 run detail types:

1. **Build artifact** — registered via `register-build-artifact` in both CloudBees and GitHub Actions workflows
2. **Deployed artifact** — registered via `register-deployed-artifact` in dedicated deploy workflows
3. **Evidence** — published via `publish-evidence-item` with a markdown build summary
4. **Test results** — Jest produces JUnit XML via `jest-junit`, uploaded via `publish-test-results`
5. **Security scan** — Trivy container image scan (GHA) and Gitleaks secrets scan (CB native)

## Workflows

### CloudBees
- `.cloudbees/workflows/cb-ci-workflow.yaml` — CI: build, test, artifact, evidence, test results, gitleaks scan
- `.cloudbees/workflows/cb-deploy-workflow.yaml` — Deploy: register deployed artifact

### GitHub Actions
- `.github/workflows/gha-ci-workflow.yaml` — CI: build, test, artifact, evidence, test results, Trivy scan
- `.github/workflows/gha-deploy-workflow.yaml` — Deploy: register deployed artifact
- `.github/workflows/gha-blackduck-scan.yaml` — Optional BlackDuck scan (workflow_dispatch only)

## Setup

Set the following on this repo before running BlackDuck workflow:
- Secret: `BLACKDUCK_API_TOKEN`
- Variable: `BLACKDUCK_SERVER_URL`

All workflows target `https://api.saas-preprod.beescloud.com`.
