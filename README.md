# QA Automation Portfolio Project

Python-based UI test automation framework using Selenium WebDriver + Behave (BDD), with cross-browser execution hooks, mobile emulation, BrowserStack capability setup, and Allure-ready results.

## Hiring Goal

No README can guarantee a job, but this one is structured to maximize interview conversion by clearly showing:

- Real automation implementation (not just theory)
- BDD design with Gherkin + step definitions
- Cross-browser and mobile-emulated coverage
- Reporting integration via Allure
- Technical self-awareness (current gaps + concrete improvement plan)

## Tech Stack

- Python 3
- Behave
- Selenium WebDriver
- WebDriver Manager
- Allure Behave Formatter
- BrowserStack (capability config + remote execution path)

## Repository Structure

```text
.
|-- browserstack.yml
|-- sample_script.py
|-- requirements.txt
|-- features
|   |-- environment.py
|   |-- tests
|   |   |-- product_search.feature
|   |   |-- first_testcase.feature
|   |   |-- second_testcase.feature
|   |   `-- second_testcase_v2.feature
|   `-- steps
|       |-- product_search.py
|       |-- first_testcase.py
|       |-- second_testcase_chrome.py
|       |-- second_testcase_firefox.py
|       `-- second_testcase_v2.py
`-- test_results
```

## What Is Automated

1. Google product search flow (`product_search.feature`)
2. Reelly sign-in + Settings -> Community navigation (`first_testcase.feature`, `second_testcase*.feature`)
3. Tagged execution profiles (`@firefox`, `@mobile`) with hook-based driver selection.

## How To Run

### 1) Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### 2) Execute tests

Run a quick smoke test:

```bash
behave features/tests/product_search.feature
```

Run cross-browser/mobile-tagged suite:

```bash
behave features/tests/second_testcase_v2.feature
```

Generate Allure-compatible output:

```bash
behave -f allure_behave.formatter:AllureFormatter -o test_results/ features/tests/second_testcase_v2.feature
```

### 3) View report (if Allure CLI is installed)

```bash
allure serve test_results
```

## Browser Behavior

`features/environment.py` uses scenario tags to choose driver strategy:

- Default: local Chrome
- `@firefox`: local Firefox
- `@mobile`: Chrome mobile emulation
- `@browserstack`: remote driver path with BrowserStack capabilities

## Code Analysis (Current State)

Strengths:

- Clean BDD separation: feature files + Python step definitions
- Explicit waits are used in the more mature scenarios (`second_testcase_v2.py`)
- Multi-environment intent is present (Chrome, Firefox, mobile emulation, BrowserStack)
- Stored run artifacts exist in `test_results/`

Gaps to fix for production-grade quality:

- Secrets are hardcoded in source/config (credentials should be environment variables)
- Mixed driver usage (`context.driver` vs `context.browser`) can break runs
- `after_scenario` performs duplicate `quit()` calls
- One step file creates/quits a global driver at import time (`first_testcase.py`)
- `sleep()` is still used in places where explicit waits should be standard
- Dependencies are unpinned (reproducibility risk)

## 7 Improvements That Strongly Increase Hiring Signal

1. Move credentials and keys to environment variables + `.env` strategy.
2. Standardize all steps on `context.driver`.
3. Refactor to Page Object Model for maintainability.
4. Replace remaining `sleep()` with explicit waits.
5. Pin dependency versions in `requirements.txt`.
6. Add CI pipeline (GitHub Actions) for automated execution and report artifacts.
7. Add negative-path and assertion-rich validations (not only navigation checks).

## Interview Talking Points

- "I implemented BDD with reusable step definitions and hook-based driver lifecycle control."
- "I designed cross-browser/mobile execution with tag-based test routing."
- "I integrated report-friendly output for Allure."
- "I can explain current framework risks and present a concrete hardening roadmap."

## Suggested Resume Bullets

- Built and maintained a Python Selenium automation framework using Behave (BDD) for web UI validation.
- Automated end-to-end user flows across Chrome, Firefox, and mobile-emulated environments.
- Implemented explicit wait strategies and assertion-driven validations to improve test reliability.
- Produced execution artifacts compatible with Allure reporting for test result transparency.

## Notes

- Replace test credentials with your own before execution.
- Do not commit secrets to Git history.
- If Firefox execution is unstable locally, verify geckodriver/browser compatibility.
