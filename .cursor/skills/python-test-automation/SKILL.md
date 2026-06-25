# Autonomous Python Test Generation & Remediation

## Intent
Automates the lifecycle of Python testing: safely scaffolds clean test modules using strict company templates, utilizes static schema payloads for mock data, runs the local runner, and repairs code until green.

## Contextual Assets
- **Scaffolding Blueprint:** `./templates/pytest_boilerplate.py.tpl`
- **Data Source of Truth:** `./resources/fallback_api_payloads.json`

## Execution Protocol

### Phase 1: Test Scaffolding
- If the task dictates writing tests for a new app file, DO NOT start from a blank file.
- Read `./templates/pytest_boilerplate.py.tpl` and duplicate its imports, fixture definitions, and AAA layout into the newly created `test_*.py` file.
- Match all test signatures to target components using the `test_` prefix required by local rules.

### Phase 2: Structural Mocking Integration
- When mocking out any remote HTTP interface or server communications, read the JSON structure inside `./resources/fallback_api_payloads.json`.
- Map the data under `auth_login_success` or `generic_api_error` directly into your `mocker.patch` return value to mimic consistent API behavior.

### Phase 3: Continuous Verification Strategy
1. Open the internal shell environment.
2. Trigger the native test runner command directly: `pytest`
3. Extract stdout logs:
   - **Scenario A (Passed):** Terminate execution cleanly, report a 100% green metric, and present the final output.
   - **Scenario B (Failed):** Read failure lines, map trace back to the relevant files, fix the bugs inside the codebase while maintaining strict compliance, and immediately re-trigger step 2.
   - Limit autonomous loop iterations to 3 attempts.