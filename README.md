# Spring Boot RabbitMQ Consumer

A simple Spring Boot application that consumes `Employee` messages from a RabbitMQ queue and validates the employee salary.

## Project Overview

This project is a Spring Boot 3.5.13 consumer service that listens to RabbitMQ messages on the queue `main.queue`.
It receives JSON representations of `Employee` objects and logs each incoming message.
If an employee salary is negative, the consumer throws an `InvalidSalaryException`.

## Key Features

- Spring Boot 3.5.13
- Java 21
- RabbitMQ message listener with JSON conversion
- Retry support for RabbitMQ listener
- Custom salary validation for incoming employee messages

## Requirements

- Java 21
- Maven 3.x
- RabbitMQ server

## Configuration

The application uses `src/main/resources/application.properties`.
Important settings:

- `server.port=8088`
- `spring.rabbitmq.listener.simple.retry.enabled=true`
- `spring.rabbitmq.listener.simple.retry.initial-interval=3s`
- `spring.rabbitmq.listener.simple.retry.max-attempts=6`
- `spring.rabbitmq.listener.simple.retry.max-interval=10s`
- `spring.rabbitmq.listener.simple.retry.multiplier=2`

The RabbitMQ listener listens on queue:

- `main.queue`

## Build and Run

1. Build the application:

   ```bash
   ./mvnw clean package
   ```

2. Run the application:

   ```bash
   ./mvnw spring-boot:run
   ```

On Windows, use `mvnw.cmd` instead:

```powershell
.\mvnw.cmd clean package
.\mvnw.cmd spring-boot:run
```

## Application Behavior

- The consumer component is `com.shaldev.service.RabbitMQConsumer`.
- The message converter is configured in `SpringbootRabbitmqConsumerApplication` using `Jackson2JsonMessageConverter`.
- Incoming messages are mapped to `com.shaldev.model.Employee`.
- Negative salary values trigger `com.shaldev.exception.InvalidSalaryException`.

## Testing

This project includes Spring Boot test dependencies. Run tests with:

```bash
./mvnw test
```

On Windows:

```powershell
.\mvnw.cmd test
```

## Notes

- Ensure RabbitMQ is running and the `main.queue` queue exists or is declared by your RabbitMQ configuration.
- The application is configured to use retries for message processing failures.
# springboot-rabbitmq-consumer
