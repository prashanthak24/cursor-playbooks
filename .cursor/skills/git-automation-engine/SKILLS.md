# Autonomous Git Commit & Verification Playbook

## Intent
Automates the safe staging, message generation, compliance formatting, and deployment-push loops for code changes within local repositories.

## Contextual Assets
- **Message Scaffolding:** `./assets/templates/commit_message_template.txt.tpl`
- **Classification Matrix:** `./assets/resources/conventional_commit_types.json`

## Execution Protocol

### Phase 1: Git Diff Audit & Context Extraction
1. Open the internal shell environment.
2. Execute `git status` and `git diff --cached` (or `git diff` if nothing is staged yet) to inspect the modified lines of code.
3. Open and parse `./resources/conventional_commit_types.json`. 
4. Based on the file paths modified, map the changes to the correct type:
   - If files match `**/test_*.py` or `**/*Test.java` ──► Type: `test`
   - If files match `**/controller/*` or `**/routes/*` ──► Type: `feat` or `fix`

### Phase 2: Structural Verification Loop (Pre-Commit Safety Gate)
1. Before committing, execute a local pre-commit verification command based on the ecosystem files found in the diff:
   - Python: `pytest`
   - Spring Boot: `./mvnw test-compile` or `./gradlew testClasses`
2. Parse stdout logs:
   - **Scenario A (Passed):** Proceed directly to Phase 3.
   - **Scenario B (Failed):** Stop immediately. Report the broken tests/compilation bugs to the user. **CRITICAL:** Do not commit or push broken code paths under any circumstances.

### Phase 3: Message Formatting & Local Commit
1. Read the structural scaffold inside `./templates/commit_message_template.txt.tpl`.
2. Generate a clean commit message utilizing the information extracted in Phase 1 and conforming to the length restrictions (e.g., subject length ≤ 50 chars).
3. Stage all verified files: `git add .` (or stage targeted changes based on the user prompt context).
4. Run the commit command passing the generated string directly: `git commit -m "[Generated Message]"`

### Phase 4: Push Safety Checks
1. Identify the current active git branch: `git branch --show-current`
2. Evaluate branch name protection rules:
   - If branch is `main`, `master`, or `develop`, abort the push step and notify the user to create a feature branch.
3. Execute the native network command: `git push origin [branch-name]`
4. Confirm successful remote state tracking to the user and exit.