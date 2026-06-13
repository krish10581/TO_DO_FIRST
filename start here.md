# Start Here — Todo App (Spring Boot)

This document explains what the project contains, how it works, how to run it, and where to find key files.

## Overview

Small, single-module Spring Boot web application that implements a simple Todo list with create, read, update, delete and toggle-completed functionality. Uses:

- Spring Boot (Web, Thymeleaf, Data JPA)
- H2 in-memory database for storage
- Thymeleaf templates for the browser UI

The app is intentionally minimal so you can extend it easily (REST endpoints, authentication, persistent DB, tests).

## Features

- Add a new task (title + optional description)
- Edit an existing task
- Delete a task (with confirmation)
- Toggle task completed state
- Simple Bootstrap-based UI

## Tech stack

- Java 17
- Spring Boot 3.x
- Spring Data JPA
- H2 (in-memory)
- Thymeleaf
- Maven

## Prerequisites

- JDK 17 installed and `JAVA_HOME` configured
- Maven installed and available on `PATH`

## Run locally

From the project root run:

```bash
mvn spring-boot:run
```

Or build and run the produced jar:

```bash
mvn package
java -jar target/todo-app-0.0.1-SNAPSHOT.jar
```

Then open http://localhost:8080 in your browser.

The H2 console is enabled (for debugging) at `http://localhost:8080/h2-console`.
JDBC URL used by the app: `jdbc:h2:mem:todos`.

## How it works (high level)

- `TodoApplication` starts the Spring context and embedded Tomcat.
- `Task` is a JPA `@Entity` that maps to an H2 table.
- `TaskRepository` extends `JpaRepository` and provides CRUD operations.
- `TodoController` handles web requests:
  - `GET /` — show list and add form (renders `index.html`)
  - `POST /add` — create a task
  - `GET /edit/{id}` — open edit form (renders `edit.html`)
  - `POST /update/{id}` — update task
  - `GET /delete/{id}` — delete and redirect
  - `POST /toggle/{id}` — toggle completed state
- Thymeleaf templates render the UI and bind form fields to the `Task` model.

## Project structure (files you will use)

- `pom.xml` — Maven build and dependencies
- `src/main/java/com/example/todo/TodoApplication.java` — application entrypoint
- `src/main/java/com/example/todo/model/Task.java` — JPA entity
- `src/main/java/com/example/todo/repository/TaskRepository.java` — Spring Data repository
- `src/main/java/com/example/todo/controller/TodoController.java` — web controller (CRUD actions)
- `src/main/resources/templates/index.html` — list + add UI
- `src/main/resources/templates/edit.html` — edit UI
- `src/main/resources/application.properties` — H2 and JPA configuration
- `README.md` — quick run instructions

## Development and extension ideas

- Add REST endpoints (`@RestController`) to expose JSON APIs for tasks.
- Add validation annotations (`@NotBlank`) and display error messages in forms.
- Replace H2 with a persistent database (Postgres/MySQL) by changing `application.properties` and JDBC driver dependency.
- Add unit/integration tests with JUnit and Spring Boot Test.
- Add user authentication (Spring Security) to isolate user tasks.

## Troubleshooting

- If the app fails to start, check the Maven build output for dependency or compilation errors.
- If templates render errors, inspect Thymeleaf expression names to ensure model attributes match.
- Use the H2 console to inspect data (`jdbc:h2:mem:todos`).

## Next steps I can do for you

- Add REST API endpoints and Postman collection
- Add unit and integration tests
- Wire a persistent database (Postgres) and sample migration
- Add Dockerfile and Docker Compose to run the app in a container

If you want any of those, tell me which one and I'll add it.
