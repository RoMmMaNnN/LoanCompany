
# LoanCompany

Multi-module Spring Boot application for loan management and related services.  
This project uses **Gradle Kotlin DSL**, **Java 21**, and **Spring Boot 3.5.10**.

---

## Project Structure

```

LoanCompany (root project)
│
├── adapter-FD        # Front Desk adapter module
├── connector-BCH     # BCH connector module
├── connector-DE      # DE connector module
├── DecisionEngine    # Decision Engine module
├── frontdesk         # Front Desk module
├── mock-bch          # Mock BCH module for testing
├── orchestrator      # Orchestrator module
├── gradle            # Gradle wrapper
├── build.gradle.kts  # Root Gradle build file
└── settings.gradle.kts

````

- Root project handles:
  - Dependency management via `dependencyManagement`
  - Spring Cloud version
  - Java toolchain configuration (Java 21)
  - Common plugins and testing configuration

- Modules contain:
  - Module-specific source code under `src/main/java` and `src/main/resources`
  - Minimal `build.gradle.kts` (mostly plugin and `java` config)
  - Module-specific tests in `src/test/java`

---

## Prerequisites

- **Java 21** (compatible with Gradle 9.x)
- **Gradle Wrapper** (run `./gradlew` from root)
- **PostgreSQL** (or configured datasource)
- Docker (for `bootBuildImage` optional)

---

## Build & Run

### Build entire project

```bash
./gradlew clean build
````

### Run a specific module

Example for Orchestrator:

```bash
cd orchestrator
../gradlew bootRun
```

> All modules are independent Spring Boot applications. Use `bootRun` per module.

### Run tests

```bash
./gradlew test
```

---

## Gradle Wrapper

The project uses the Gradle wrapper located in the `gradle/wrapper` directory:

```bash
./gradlew wrapper
```

This ensures everyone builds with the same Gradle version.

---

## Docker Image (optional)

```bash
./gradlew bootBuildImage
```

* Produces a container image for the module being built
* Uses Paketo buildpacks: `paketobuildpacks/ubuntu-noble-run:latest`

---

## Notes

* Multi-module setup allows each service to evolve independently
* Root project manages shared dependencies and Spring Cloud version
* Use `settings.gradle.kts` to add/remove modules:

```kotlin
include(
    "adapter-FD",
    "connector-BCH",
    "connector-DE",
    "DecisionEngine",
    "frontdesk",
    "mock-bch",
    "orchestrator"
)
```

* Keep module `build.gradle.kts` minimal; root project handles most dependencies

---

## License

This project is internal and proprietary. Unauthorized use is prohibited.
