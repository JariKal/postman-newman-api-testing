# Postman & Newman API Testing Portfolio

API testing portfolio demonstrating practical REST API testing with Postman and Newman, using the ALT Zone development API.

## Project Overview

This project demonstrates my experience in manual API testing, test execution, regression testing, troubleshooting, and interpreting test results.

The Postman collection contains 34 API requests organized into 10 folders. Newman is used to execute the same collection from the command line and generate test reports.

## Tools

- **Postman** – API requests, test cases, response validation, and debugging.
- **Newman 6.2.2** – Command-line execution of the Postman collection.
- **Newman HTML Extra Reporter 1.23.1** – HTML test reporting.
- **PowerShell** – Environment setup and command-line execution.
- **AI assistance** – Support with test scripting, configuration, troubleshooting, and documentation.

## Test Coverage

The collection includes:

- Authentication and smoke testing
- Authorization testing with missing, invalid, and insufficient credentials
- Profile, Player, Clan, Room, Item, Stock, and Soulhome endpoints
- Positive and negative test scenarios
- HTTP status code validation (200, 201, 400, 401, 403, and 404)
- JSON response validation
- Response field and data type verification
- Dynamic ID extraction and validation

The collection uses a test account and automatically stores authentication tokens and relevant IDs during execution.

## Test Results

One verified Newman regression run produced the following results:

| Metric | Result |
|---|---|
| API requests | 34 / 34 passed |
| Test scripts | 34 / 34 executed successfully |
| Assertions | 227 / 227 passed |
| Failed assertions | 0 |
| Total run duration | 4.6 seconds |
| Average response time | 46 ms |

All checks passed in this run. Results may vary as the development API changes.

An additional Newman run with HTML Extra reporting also completed successfully.

## How to Run

### 1. Requirements

Install Node.js, Newman, and optionally the HTML Extra reporter.

```powershell
npm install -g newman@6.2.2
npm install -g newman-reporter-htmlextra@1.23.1
```

### 2. Configure the environment

Import `environment.example.json` into Postman or use it with Newman.

Set the `username` and `password` values locally for an authorized ALT Zone development API test account.

Do not commit credentials, authentication tokens, or private environment files to GitHub.

### 3. Run in Postman

Import the Postman collection and example environment, configure your test account, and run the entire `Regression Portfolio` folder using Postman's Collection Runner.

### 4. Run with Newman

After configuring an authorized test environment, execute:

```powershell
newman.cmd run "ALT Zone API Regression Portfolio.postman_collection.json" -e "environment.example.json" -r cli
```

The example environment has empty credentials, so authenticated tests require valid local credentials before running.

### 5. Generate an HTML report

```powershell
newman.cmd run "ALT Zone API Regression Portfolio.postman_collection.json" -e "environment.example.json" -r cli,htmlextra --reporter-htmlextra-export "ALT-Zone-Regression-Report.html"
```

HTML reports may contain sensitive request and response information. Review and sanitize them before sharing.

## AI-Assisted Testing

This project was developed with the assistance of AI tools.

**Postman**

- AI assisted in writing and improving test scripts.
- I executed tests, examined API responses, investigated failures, and verified test results.

**Newman**

- AI assisted with command-line configuration, troubleshooting, and test execution instructions.
- I ran regression tests, worked through environment configuration problems with AI guidance, and verified the results.

My primary background is in manual software testing. I use AI to support technical tasks and learn automation tools, rather than claiming to have independently written all test automation scripts.

## Security

- No real usernames, passwords, or authentication tokens are included in the published collection.
- The example environment contains empty credential values.
- The tests are intended for authorized use against the ALT Zone development API.
- Actual credentials and generated HTML reports are kept private.

## Project Context

ALT Zone is a game project developed by Psyche's Royale Gaming ry. This repository is an independent testing portfolio example focused on API testing practices.
