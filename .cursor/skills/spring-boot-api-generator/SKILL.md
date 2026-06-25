# Autonomous Spring Boot Feature Generation Playbook

## Intent
Automates the lifecycle of creating a Spring Boot REST API endpoint: provisions immutable Record DTOs, sets up Controller templates, hooks in Service layer dependencies, and compiles locally to ensure zero build breakages.

## Contextual Assets
- **Scaffolding Blueprint:** `.assets/templates/spring_controller_template.java.tpl`
- **Data Error Schema:** `.assets/resources/standard_error_response.json`

## Execution Protocol

### Phase 1: Requirement Extraction & Rule Contextualization
- Parse the user's requirements to determine fields, resource names, data paths, and layer placement.
- **Mandatory Quality Check:** Read the raw file contents of `./.cursor/rules/spring-boot-api-standards.mdc`. Extract instructions regarding Java `record` types, banning `@Autowired` field injection, and using `ResponseEntity`. Ensure your code generation plan fully complies.

### Phase 2: Code Generation Sequence
1. **DTO Generation:** Create the request and response payload structures as immutable Java `record` types using `jakarta.validation` metadata rules.
2. **Controller Scaffolding:** Read `./templates/spring_controller_template.java.tpl`. Duplicate its structure, replace placeholding terms with your real types, and drop it inside the proper project package path.
3. **Service Layer Provisioning:** Generate or append to the matching Service class. Inject dependencies using explicit constructor declarations (or Lombok `@RequiredArgsConstructor`). Ensure operations return typed objects, never raw entities.

### Phase 3: Build Verification & Quality Assurance Strategy
1. Open the local terminal/shell environment.
2. Detect the build orchestration engine by searching for `pom.xml` or `build.gradle`.
3. Run the compiler verification suite command directly:
   - For Maven: `./mvnw clean test-compile` (or `mvn test-compile`)
   - For Gradle: `./gradlew testClasses` (or `gradle testClasses`)
4. Extract stdout/stderr logs from the terminal:
   - **Scenario A (Passed Verification):** Code compiles perfectly with zero dependency breaks. Complete the task by displaying the created structures to the user.
   - **Scenario B (Failed Verification):** If the compiler throws type mismatches, missing imports, or annotation processing failures, capture the line number. Refactor the code paths to fix bugs while continuing to strictly follow the code rules in Phase 1.
   - Limit autonomous iteration cycles to 3 loops before stopping to ask the developer.