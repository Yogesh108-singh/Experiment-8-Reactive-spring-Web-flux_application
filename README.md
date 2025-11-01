# Reactive Spring WebFlux Application

A small example Reactive application built with **Spring WebFlux** and **Project Reactor**. This project demonstrates building non-blocking REST APIs that return `Flux` and `Mono` types for reactive streaming. It includes endpoints for fetching all products and a single product.

---

## Table of Contents

* [Features](#features)
* [Prerequisites](#prerequisites)
* [Project structure](#project-structure)
* [How to run](#how-to-run)
* [Available endpoints](#available-endpoints)
* [Examples (cURL)](#examples-curl)
* [Testing](#testing)
* [Build & packaging](#build--packaging)
* [Troubleshooting](#troubleshooting)
* [Contributing](#contributing)
* [License](#license)

---

## Features

* Reactive REST API using Spring WebFlux
* Example `Product` model with endpoints:

  * Get all products (`Flux<Product>`)
  * Get single product by id (`Mono<Product>`)
* Basic in-memory data source (replaceable with reactive DB later)
* Simple service and controller layers demonstrating reactive patterns

---

## Prerequisites

* Java 17 or newer (verify with `java -version`)
* Maven 3.6+ (verify with `mvn -v`)
* An IDE such as IntelliJ IDEA or VS Code (optional)

---

## Project structure

```
Experiment-8-Reactive-spring-Web-flux_application/
├── src/
│   ├── main/
│   │   ├── java/com/example/reactive/         # application packages
│   │   │   ├── controller/                    # REST controllers
│   │   │   ├── model/                         # domain objects (Product)
│   │   │   ├── repository/                    # in-memory or reactive repo
│   │   │   └── service/                       # business logic
│   │   └── resources/
│   │       └── application.yml                # configuration
├── pom.xml
└── README.md
```

---

## How to run

From the project root (where `pom.xml` is located):

```bash
# build the project
mvn clean package

# run using spring-boot plugin
mvn spring-boot:run

# or run the generated jar
java -jar target/<artifactId>-<version>.jar
```

If you are using the path on your machine:

```bash
cd "C:\Users\lenovo\Desktop\YOG\Experiment-8-Reactive-spring-Web-flux_application"
mvn spring-boot:run
```

---

## Available endpoints

> Base path: `/api` (adjust if your app uses a different base path)

* `GET /api/products` — returns a stream/list of all products (HTTP 200)
* `GET /api/products/{id}` — returns a single product by id (HTTP 200) or 404 if not found

> Responses are JSON and reactive (Flux/Mono). Replace paths in examples below if your controller mapping differs.

---

## Examples (cURL)

Get all products:

```bash
curl -s http://localhost:8080/api/products | jq .
```

Get a single product (id = 1):

```bash
curl -s http://localhost:8080/api/products/1 | jq .
```

If the endpoint streams elements (Server-Sent Events) you can request with `Accept: text/event-stream`.

---

## Testing

* Unit tests: use JUnit and Reactor Test (`StepVerifier`) for service-layer reactive flows.
* Integration tests: use `@SpringBootTest` with `WebTestClient` to exercise WebFlux endpoints.

Example snippet for `WebTestClient`:

```java
@Autowired
private WebTestClient webTestClient;

@Test
void getAllProducts_returnsList() {
  webTestClient.get().uri("/api/products")
    .exchange()
    .expectStatus().isOk()
    .expectBodyList(Product.class).hasSizeGreaterThan(0);
}
```

---

## Build & packaging

* Build a fat jar: `mvn clean package`
* Use Docker: add a `Dockerfile` that runs the jar with `java -jar` (optional)

---

## Troubleshooting

* `mvn` not recognized: make sure Maven is installed and added to PATH. On Windows, restart your terminal after updating PATH.
* Port conflicts: change `server.port` in `application.yml` or stop the process using the port.
* Class not found / package mismatch: confirm the package names match the `@SpringBootApplication` main class location.

---

## Contributing

Contributions are welcome. Suggested workflow:

1. Fork the repository
2. Create a feature branch (`git checkout -b feat/my-feature`)
3. Commit changes and open a Pull Request

Please follow simple code style and write unit tests for new behavior.

---

## License

This project is provided under the MIT License. Replace with your preferred license if needed.

---

If you want, I can:

* Add badges (build, license, java version)
* Create a `Dockerfile` example
* Add example unit tests or a `data.sql`/`data.json` seed file

Tell me which to add and I will update the README.
