# Booking Microservices NestJS

A distributed microservices architecture built with NestJS, implementing Vertical Slice Architecture, Event-Driven Architecture, CQRS, PostgreSQL with TypeORM, RabbitMQ, and OpenTelemetry.

---

## Architectural Principles

### Vertical Slice Architecture & REPR Pattern
Instead of traditional monolithic layered structures, this project organizes functionality into vertical slices around business features. Each slice encapsulates its route, request handling, business logic, persistence, and response handling.

By decoupling features into independent slices:
* High cohesion within each business capability.
* Low coupling between unrelated features.
* Simplified maintenance and testing.

### Command Query Responsibility Segregation (CQRS)
Using NestJS `@nestjs/cqrs`, read operations (queries) are separated from write operations (commands):
* **Commands**: Handle business logic and data mutations.
* **Queries**: Optimised data retrieval with minimal overhead.
* **Events**: Internal domain events and inter-service integration events published via RabbitMQ.

---

## Services Architecture

| Service | Port | Description | Persistence |
| :--- | :--- | :--- | :--- |
| **Identity Service** | `3333` | Authentication, JWT management, and User accounts | PostgreSQL (`identity`) |
| **Flight Service** | `3344` | Airports, Aircraft, Flight scheduling, and Seat inventory | PostgreSQL (`flight`) |
| **Passenger Service** | `3355` | Passenger profile management | PostgreSQL (`passenger`) |
| **Booking Service** | `3366` | Flight reservation and booking processing | PostgreSQL (`booking`) |

---

## Getting Started

### Infrastructure Setup

Start the required infrastructure (PostgreSQL, RabbitMQ, OpenTelemetry Collector, Prometheus, Tempo, Loki, Grafana) using Docker Compose:

```bash
docker-compose -f ./deployments/docker-compose/infrastructure.yaml up -d
```

### Full Application Stack

To launch all microservices along with infrastructure via Docker Compose:

```bash
docker-compose -f ./deployments/docker-compose/docker-compose.yaml up -d
```

---

## Development Workflow

### Building Services
To build a microservice, execute the following within the service directory:

```bash
npm run build
```

### Running Services
To run a microservice in watch mode:

```bash
npm run dev
```

### Database Migrations
Migrations are managed per service using TypeORM.

* **Generate Migration**:
  ```bash
  npm run migration:generate -- src/data/migrations/migration-name
  ```
* **Run Migrations**:
  ```bash
  npm run migration:run
  ```
* **Revert Migration**:
  ```bash
  npm run migration:revert
  ```

---

## Testing

Execute unit and integration tests within each microservice directory:

```bash
npm run test
```

Interactive REST requests are also available in [booking.rest](./booking.rest) for use with REST Client extensions.

---

## API Documentation

Each microservice exposes an interactive OpenAPI (Swagger) interface when running:
* **Identity API**: `http://localhost:3333/swagger`
* **Flight API**: `http://localhost:3344/swagger`
* **Passenger API**: `http://localhost:3355/swagger`
* **Booking API**: `http://localhost:3366/swagger`

---

## Contribution

Please review the [Contribution Guidelines](./CONTRIBUTION.md) before submitting pull requests or opening issues.

---

## License

This project is licensed under the [MIT License](./LICENSE).
