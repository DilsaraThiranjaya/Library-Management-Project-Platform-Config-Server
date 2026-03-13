# Platform: Config Server

This repository contains the Spring Boot Config Server for the Library Management System.

## Architectural Purpose

In a distributed microservices environment, managing configurations locally across multiple instances and environments becomes complex and error-prone. This **Config Server** solves that problem by acting as a centralized control plane for externalized configuration properties across all applications in all environments.

It integrates directly with the [`Library-Management-Project-Configurations`](https://github.com/DilsaraThiranjaya/Library-Management-Project-Configurations) Git repository to serve dynamic configurations to the other microservices in real-time.

## Technical Stack

- **Java**: 25
- **Spring Boot**: 4.0.3
- **Spring Cloud**: 2025.1.0
- **Build Tool**: Maven
- **Group ID**: `lk.ijse.eca`

### Key Dependencies

- `spring-cloud-config-server`: Enables the core centralized server mechanics.
- `spring-cloud-starter-netflix-eureka-client`: Allows the Config Server itself to register with the Service Registry so other services can discover it programmatically.
- `spring-boot-starter-actuator`: Exposes endpoints for monitoring runtime health and operational status.
- `spring-boot-devtools`: Facilitates rapid application development by enabling auto-restarts on code changes.

## Default Configuration

The application is configured out-of-the-box (in `application.yml`) to:
1. Run on port: `8888`
2. Look up configuration properties from the Git URI: `https://github.com/DilsaraThiranjaya/Library-Management-Project-Configurations.git` (specifically the `main` branch).
3. Search for property files mapped to the requesting service's application name (`{application}`).
4. Register with a local Eureka Discovery Server at `http://localhost:8761/eureka/`.

## Running the Application

Before starting the Config Server, ensure that you have initialized the `Library-Management-Project-Configurations` repository, as this server will attempt to read from it upon startup.

```bash
# Provide necessary GitHub or SSH credentials if the Configurations repo is private
mvn spring-boot:run
```

Once running, any microservice configured to communicate with the Config Server will contact this application at startup to fetch its environment-specific settings.