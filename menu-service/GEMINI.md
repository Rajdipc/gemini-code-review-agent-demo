# Menu Service Project Overview

This project is a Java-based RESTful microservice built with the Quarkus framework. Its primary function is to manage menu items, providing a comprehensive set of CRUD (Create, Read, Update, Delete) operations through RESTful API endpoints. The service also allows for filtering menu items based on their processing status (Ready, Failed, Processing).

## Technologies Used

*   **Framework:** Quarkus
*   **Build Tool:** Apache Maven
*   **Web Layer:** RESTEasy (Quarkus extension for JAX-RS)
*   **Persistence:** Hibernate ORM with Panache
*   **Database:** H2 (in-memory for development/testing), PostgreSQL (for production/external databases)
*   **Testing:** JUnit 5, Mockito, Rest-Assured
*   **Containerization:** Jib (for building Docker images)

## Project Structure

*   `src/main/java/org/google/demo`: Contains the core Java source code for the menu service, including REST resources, entities, and repositories.
*   `src/main/resources`: Contains application configuration (e.g., `application.properties`).
*   `src/test/java/org/google/demo`: Contains unit and integration tests.
*   `pom.xml`: Maven project object model, defining dependencies, build processes, and plugins.
*   `mvnw`, `mvnw.cmd`: Maven wrapper scripts for consistent build environments.

## Building and Running

### Build the project

To compile and package the application:

```bash
./mvnw clean package
```

### Run in development mode

You can run your application in development mode that enables live coding:

```bash
./mvnw quarkus:dev
```

### Run tests

To run all tests:

```bash
./mvnw test
```

To run integration tests (if any are specifically configured with Failsafe):

```bash
./mvnw verify -Pnative # This profile is for native image builds, which includes integration tests
```

### Create a native executable

You can create a native executable using GraalVM. This requires GraalVM to be installed and configured.

```bash
./mvnw clean package -Pnative
```

### Create a Docker image

The project is configured to use Jib for building Docker images. To build a Docker image:

```bash
./mvnw compile jib:build
```

## Development Conventions

*   **Coding Style:** Standard Java and Quarkus conventions are followed.
*   **API Design:** RESTful principles are used for designing the API endpoints.
*   **Testing:** Unit and integration tests are written using JUnit 5 and Rest-Assured.
*   **Configuration:** Application properties are managed via `src/main/resources/application.properties`.
