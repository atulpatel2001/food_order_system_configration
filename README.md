# Food Order System - Configuration Repository

This repository is dedicated to storing the **configuration files** for the Food Order System microservices. The configurations are fetched dynamically by the **Spring Cloud Config Server**, ensuring centralized and version-controlled application settings.

## Overview

- This repository contains **YAML/Properties** configuration files for each microservice.
- The **Spring Cloud Config Server** reads these configurations and serves them to the respective services at runtime.
- Configuration updates can be **refreshed dynamically** using **Spring Cloud Bus** with RabbitMQ.

## Microservices Using This Configuration Repository

1. **User Service** - Handles authentication and user management
2. **Address Management Service** - Manages user addresses
3. **Eureka Service** - Manages eureka server
4. **Api Gateway Service** - handle all service endpoint
5. 
## Structure of the Repository

```
/config-repo
│── application.yml (Global configurations)
│── user-service.yml (User service-specific configurations)
│── address-service.yml (Address management configurations)
│── eureka-service.yml (eureka server related configurations)
│── gateway-service.yml (api gateway configurations)
```

## Fetching Configurations via Config Server

### **1. Start the Config Server**
Ensure the **Spring Cloud Config Server** is running on port `8071`.

```bash
mvn spring-boot:run
```

### **2. Fetch Configuration for a Specific Service**
You can retrieve a specific service's configuration by hitting the following endpoint:

```
GET http://localhost:8071/user-service/default
```

### **3. Refresh Configuration Dynamically**
If you make changes in the configuration repository and want to refresh the services without restarting them, trigger a refresh event:

```bash
POST http://localhost:8080/actuator/bus-refresh
```

> Ensure RabbitMQ is running for this to work properly.

## Setting Up the Config Server to Use This Repository
In the **Config Server's `application.yml`**, specify the GitHub URL for this repository:

```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/your-org/food-order-config-repo
          clone-on-start: true
```
---
This repository plays a crucial role in managing configurations for all microservices in the Food Order System. 🚀

