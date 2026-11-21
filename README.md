# java-junit-testing

A JUnit 5 test suite over a contact entity and its service layer — the part of a program
you do not ship, and the part that tells you whether the rest of it works.

> Coursework from my B.S. in Computer Science (Southern New Hampshire University). The implementation and the written test
> strategy are mine; the assignment brief was the original prompt.

## What it does

Two production classes and two test classes:

- **`Contact`** — a contact record with a fixed ID. Every field is validated in the
  constructor and in the setters: null checks, length limits, and a 10-digit phone check,
  each raising `IllegalArgumentException`.
- **`ContactService`** — a `HashMap`-backed store with `addContact`, `getContact`,
  `deleteContact`, and per-field update methods, each rejecting unknown or duplicate IDs.
- **`ContactTest` / `ContactServiceTest`** — the suites covering both.

## What it demonstrates

- **Defensive input validation** — invalid state is rejected at construction rather than
  discovered later.
- **Unit test design** — one test per behaviour, named for the behaviour
  (`testCreateContactContactIdTooLong`), covering the happy path and each failure mode.
- **Service-layer contracts** — duplicate IDs rejected, missing IDs rejected, updates
  applied and observable through the accessor.
- **Test strategy** — a written strategy (in the reflection) covering unit, integration,
  and system levels, plus code review and security practice.

## Tech

Java, JUnit 5 (`org.junit.jupiter`). No build system is checked in — the four files are
plain `javac` sources.

## Running it

```bash
# JUnit's standalone console launcher — one jar, no build tool needed
curl -Lo junit-platform-console-standalone.jar \
  https://repo1.maven.org/maven2/org/junit/platform/junit-platform-console-standalone/1.10.2/junit-platform-console-standalone-1.10.2.jar

javac -cp junit-platform-console-standalone.jar \
  Contact.java ContactService.java ContactTest.java ContactServiceTest.java

java -jar junit-platform-console-standalone.jar --class-path . --scan-classpath
```

## Files

| File | What it is |
|---|---|
| `Contact.java` | Entity: field validation, getters, guarded setters |
| `ContactService.java` | Service layer over a `HashMap` store |
| `ContactTest.java` | Unit tests for the entity |
| `ContactServiceTest.java` | Unit tests for the service layer |
| `Module 7 - Project 2.docx` | Written test strategy and reflection |
