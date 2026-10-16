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

Install Node.js and Newman. HTML Extra Reporter is optional.

```powershell
npm install -g newman@6.2.2
npm install -g newman-reporter-htmlextra@1.23.1
```

### 2. Configure the environment

The repository includes `environment.example.json` with the required environment variable names and no credentials.

Import the collection and example environment into Postman. For Postman testing, enter the credentials of an authorized development test account locally.

For Newman, use PowerShell to provide credentials without saving them in the repository.

### 3. Run tests in Postman

1. Import the collection and `environment.example.json`.
2. Select the imported environment and configure the test account credentials locally.
3. Open the Collection Runner.
4. Run the entire `Regression Portfolio` folder, starting with authentication.

### 4. Run tests with Newman

Open PowerShell in the directory containing the collection and example environment.

Enter the following commands:

```powershell
$env:ALTZONE_BASE_URL = "https://devapi.altzone.fi"
$env:ALTZONE_TEACHER_URL = "https://devapi.altzone.fi/teacher"

$env:ALTZONE_USERNAME = Read-Host "Test account username"

$securePassword = Read-Host "Test account password" -AsSecureString
$env:ALTZONE_PASSWORD = [System.Net.NetworkCredential]::new("", $securePassword).Password
Remove-Variable securePassword
```

Then execute the collection:

```powershell
newman.cmd run "ALT Zone API Regression Portfolio.postman_collection.json" `
  -e "environment.example.json" `
  --env-var "baseUrl=$env:ALTZONE_BASE_URL" `
  --env-var "teacherBaseUrl=$env:ALTZONE_TEACHER_URL" `
  --env-var "username=$env:ALTZONE_USERNAME" `
  --env-var "password=$env:ALTZONE_PASSWORD" `
  -r cli
```

### 5. Generate an HTML report

Run the same collection with HTML Extra Reporter:

```powershell
newman.cmd run "ALT Zone API Regression Portfolio.postman_collection.json" `
  -e "environment.example.json" `
  --env-var "baseUrl=$env:ALTZONE_BASE_URL" `
  --env-var "teacherBaseUrl=$env:ALTZONE_TEACHER_URL" `
  --env-var "username=$env:ALTZONE_USERNAME" `
  --env-var "password=$env:ALTZONE_PASSWORD" `
  -r cli,htmlextra `
  --reporter-htmlextra-export "ALT-Zone-Regression-Report.html"
```

**Security notes:** Password input is masked and is not saved to PowerShell command history as literal text. However, these commands pass credentials through process arguments, which may be visible to local process-monitoring tools. The password also remains in the PowerShell process environment until cleared or the session ends. Use only dedicated test credentials.

After testing, clear the variables:

```powershell
Remove-Item Env:ALTZONE_USERNAME, Env:ALTZONE_PASSWORD -ErrorAction SilentlyContinue
```

HTML reports may contain sensitive request or response data, including authentication tokens. Keep generated reports private unless carefully sanitized.

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
