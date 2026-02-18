# Menu Service - A Quarkus-based RESTful API

Welcome to the Menu Service! This is a RESTful service built with Quarkus that allows you to manage items on a restaurant menu.

[![Made with Quarkus](https://img.shields.io/badge/Made%20with-Quarkus-4695eb.svg)](https://quarkus.io/)

## Overview

The Menu Service provides a set of API endpoints to perform CRUD (Create, Read, Update, Delete) operations on menu items. It's a simple yet powerful demonstration of how to build modern, cloud-native Java applications with Quarkus.

The service uses Panache for simplified Hibernate ORM, RESTEasy for creating REST endpoints, and can be easily containerized with Jib.

### Architecture

The service follows a simple layered architecture:

```
   +----------------+      +------------------+      +----------------+
   |   JAX-RS       |      |    Panache       |      |  PostgreSQL /  |
   | (MenuResource) | <--> | (MenuRepository) | <--> |       H2       |
   +----------------+      +------------------+      +----------------+
         |
         v
   +------------+
   | Panache    |
   | (Menu Entity)|
   +------------+
```

*   **`MenuResource.java`**: The JAX-RS resource that exposes the REST API endpoints.
*   **`MenuRepository.java`**: The Panache repository that handles database operations for the `Menu` entity.
*   **`Menu.java`**: The Panache entity representing a menu item in the database.
*   **`Status.java`**: An enum representing the status of a menu item.

## API Endpoints

The following endpoints are available under the `/menu` path:

*   `GET /`: Retrieves all menu items.
*   `GET /{id}`: Retrieves a specific menu item by its ID.
*   `GET /ready`: Retrieves all menu items with the status `Ready`.
*   `GET /failed`: Retrieves all menu items with the status `Failed`.
*   `GET /processing`: Retrieves all menu items with the status `Processing`.
*   `POST /`: Creates a new menu item.
*   `PUT /{id}`: Updates an existing menu item.
*   `DELETE /{id}`: Deletes a menu item.

### Menu Item Data Model

A menu item has the following attributes:

| Field              | Type         | Description                                     | Constraints          |
| ------------------ | ------------ | ----------------------------------------------- | -------------------- |
| `id`               | `Long`       | The unique identifier for the menu item.        |                      |
| `itemName`         | `String`     | The name of the menu item.                      |                      |
| `itemPrice`        | `BigDecimal` | The price of the menu item.                     |                      |
| `spiceLevel`       | `int`        | The default spice level.                        |                      |
| `tagLine`          | `String`     | A short tagline for the item.                   |                      |
| `itemImageUrl`     | `URL`        | URL for the item's image.                       |                      |
| `itemThumbnailUrl` | `URL`        | URL for the item's thumbnail image.             |                      |
| `status`           | `Status`     | The status of the item (`Processing`, `Ready`, `Failed`). | |
| `description`      | `String`     | A description of the item.                      |                      |
| `rating`           | `Integer`    | The rating of the item.                         | `@NotNull`, `@Min(1)`, `@Max(5)` |
| `createDateTime`   | `LocalDateTime` | Timestamp of when the item was created.      | `@CreationTimestamp` |
| `updateDateTime`   | `LocalDateTime` | Timestamp of the last update.                | `@UpdateTimestamp`   |

## Getting Started

### Prerequisites

*   JDK 11+
*   Maven 3.8.1+

### Running the application in dev mode

You can run your application in dev mode that enables live coding using:

```shell
cd menu-service
./mvnw compile quarkus:dev
```

> **_NOTE:_** Quarkus now ships with a Dev UI, which is available in dev mode only at http://localhost:8080/q/dev/.

### Packaging and running the application

The application can be packaged using:

```shell
./mvnw package
```

It produces the `quarkus-run.jar` file in the `target/quarkus-app/` directory.
Be aware that it is not an _über-jar_ as the dependencies are copied into the `target/quarkus-app/lib/` directory.

The application is now runnable using `java -jar target/quarkus-app/quarkus-run.jar`.

### Creating a native executable

You can create a native executable using:

```shell
./mvnw package -Pnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using:

```shell
./mvnw package -Pnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/menu-service-1.0.0-runner`



