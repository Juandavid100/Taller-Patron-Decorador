# 🐎 HorseCare

HorseCare is a small web application created as a practical example of the **Decorator Design Pattern** using **Java and Spring Boot**.

The application represents a real-world equestrian care scenario: a basic horse-care service can be dynamically extended with additional services such as premium food, bathing, training and veterinary check-ups.

---

## 🎯 Purpose

The main purpose of this project is to demonstrate how the Decorator pattern allows additional responsibilities to be added to an object dynamically without modifying its original class.

Instead of creating a separate class for every possible combination of services, HorseCare wraps the base service with different decorators.

Example:

```text
BasicHorseCare
      ↓
PremiumFoodDecorator
      ↓
BathDecorator
      ↓
TrainingDecorator
```

---

## 🧩 Decorator Pattern

The project contains the following roles:

### Component

`HorseService`

Defines the common operations:

- `getDescription()`
- `getPrice()`

### Concrete Component

`BasicHorseCare`

Represents the original/base service.

### Base Decorator

`HorseServiceDecorator`

Keeps a reference to another `HorseService` and delegates its behavior.

### Concrete Decorators

- `PremiumFoodDecorator`
- `BathDecorator`
- `TrainingDecorator`
- `VeterinaryDecorator`

Each decorator adds its own description and price.

---

## 💰 Service prices

| Service | Price |
|---|---:|
| Basic horse care | $80.000 |
| Premium food | +$30.000 |
| Bath and grooming | +$20.000 |
| Training | +$50.000 |
| Veterinary check-up | +$40.000 |

Prices are examples created for the academic demonstration.

---

## 🛠️ Technologies

- Java 21
- Spring Boot 3.5.6
- Maven
- HTML5
- CSS3
- JavaScript
- REST API

No database is required.

---

## 📁 Project structure

```text
HorseCare/
│
├── src/
│   └── main/
│       ├── java/
│       │   └── com/horsecare/
│       │       ├── HorseCareApplication.java
│       │       ├── controller/
│       │       │   └── HorseController.java
│       │       ├── model/
│       │       │   ├── HorseService.java
│       │       │   └── BasicHorseCare.java
│       │       └── decorator/
│       │           ├── HorseServiceDecorator.java
│       │           ├── PremiumFoodDecorator.java
│       │           ├── BathDecorator.java
│       │           ├── TrainingDecorator.java
│       │           └── VeterinaryDecorator.java
│       │
│       └── resources/
│           └── static/
│               ├── index.html
│               ├── style.css
│               └── script.js
│
├── pom.xml
└── README.md
```

---

## ▶️ How to run

### Requirements

Install:

- Java 21 or compatible JDK
- Maven 3.9+ (optional if using the Maven Wrapper or an IDE with Maven support)
- IntelliJ IDEA, Eclipse or Visual Studio Code can be used as the IDE.

Verify Java:

```bash
java -version
```

The project was configured for Java 21.

### Run with Maven

Open a terminal inside the `HorseCare` folder and execute:

```bash
mvn spring-boot:run
```

Then open:

```text
http://localhost:8080
```

### Build the project

```bash
mvn clean package
```

Run the generated JAR:

```bash
java -jar target/horsecare-1.0.0.jar
```

---

## 🔌 REST API

The frontend communicates with the backend through:

```text
POST /api/services/calculate
```

Example request:

```json
{
  "premiumFood": true,
  "bath": true,
  "training": false,
  "veterinary": true
}
```

The backend creates the service dynamically:

```java
HorseService service = new BasicHorseCare();

if (request.premiumFood()) {
    service = new PremiumFoodDecorator(service);
}

if (request.bath()) {
    service = new BathDecorator(service);
}

if (request.training()) {
    service = new TrainingDecorator(service);
}

if (request.veterinary()) {
    service = new VeterinaryDecorator(service);
}
```

The final object contains all selected decorators.

---

## ☁️ Deployment

The project is designed to be deployable to a cloud platform that supports Java/Spring Boot applications.

For deployment, the application listens on the platform-provided `PORT` only if the platform is configured to provide one. For a production deployment, the Spring server port can be configured with:

```text
server.port=${PORT:8080}
```

This can be added to:

```text
src/main/resources/application.properties
```

The project currently uses port `8080` locally.

---

## 📚 Academic explanation

### Problem

A horse-care center may offer a basic service and several optional services. The combinations can grow quickly.

For example:

```text
Basic
Basic + Food
Basic + Bath
Basic + Food + Bath
Basic + Food + Training
Basic + Food + Bath + Training
...
```

Creating a class for every possible combination would make the system difficult to maintain.

### Solution

The Decorator pattern allows each optional service to wrap another service.

```text
HorseService
    ↑
BasicHorseCare

HorseServiceDecorator
    ↑
    ├── PremiumFoodDecorator
    ├── BathDecorator
    ├── TrainingDecorator
    └── VeterinaryDecorator
```

This makes the system flexible and allows combinations to be created at runtime.

---

## 👨‍💻 Author

Academic project — Software Engineering.

HorseCare was created as a practical implementation of the **Decorator Design Pattern** using Java and Spring Boot.
