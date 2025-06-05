# Design Patterns in the Smart Kitchen System

This document outlines the core software and system design patterns leveraged in the Smart Kitchen prototype. While no actual code has been implemented, the architecture and logic design follow well-established design principles in software engineering and embedded systems to promote modularity, scalability, and maintainability.

---

## 1. Model-View-Controller (MVC)

The MVC architectural pattern is conceptually adopted to separate concerns within the Smart Kitchen system:

- **Model:**  
  The Oracle database stores all structured data including nutritional profiles, historical user logs, and system configurations. It acts as the central data model the system depends on.

- **View:**  
  The touchscreen LCD tablet serves as the primary user interface (UI). It visualizes nutritional information, provides real-time feedback, and presents recommendations to the user.

- **Controller:**  
  The microcontroller processes raw input from sensors (e.g., barcode data, image recognition, and weight readings), interprets this data, and coordinates communication between the database and the LCD display.

This separation ensures that changes in the UI or data layer can be made independently, improving maintainability.

---

## 2. Observer Pattern

The system uses an event-driven logic flow akin to the Observer Pattern:

- **Sensors** (weight sensor, barcode scanner, CMOS camera) act as **subjects**.
- The **controller and display** components act as **observers**.

Whenever a change is detected (e.g., new food item placed), the sensors notify the controller, which triggers a chain of updates:
- Fetch data from the database
- Calculate the nutritional profile
- Push real-time feedback to the user interface

This approach supports a responsive, real-time user experience with minimal user interaction.

---

## 3. Client-Server Pattern

A classic **Client-Server** model underpins the architecture:

- **Client:** The Smart Kitchen device (sensors + microcontroller) collects data and sends requests for processing.
- **Server:** The backend handles logic, processes data, and retrieves records from the Oracle DB.
- Communication is conducted over HTTP using JSON-encoded data.

This pattern allows for scalable integrations (e.g., with external apps like MyFitnessPal) and ensures separation between the data processing logic and the user-facing interface.

---

## 4. Repository Pattern

Data interactions with the Oracle database are abstracted conceptually via a repository layer:

- Rather than interacting directly with SQL queries from the microcontroller logic, the system assumes an intermediate backend (e.g., Python Flask or Node.js API) that retrieves and updates data.
- This decouples data access from business logic and allows for easier schema updates or changes to the database engine in future versions.

---

## 5. Strategy Pattern (Recommender Logic)

The recommender system for low-calorie alternatives employs a Strategy-like conceptual design:

- When presenting food options, the system evaluates whether the current food item exceeds a 100 kcal per 100g threshold.
- If so, it uses a set of predefined strategies (based on nutritional goals) to suggest lower-calorie alternatives.
- These strategies can be swapped or updated based on user goals (e.g., fat loss, muscle gain).

This flexible structure ensures that recommendations remain adaptable without changing the core system logic.

---

## 6. Adapter Pattern (App Integration)

To support **synchronisation with nutrition apps and fitness trackers**, the system design implies use of the Adapter Pattern:

- Each third-party app (e.g., MyFitnessPal, Google Fit) may have different API formats.
- Adapter components would be required to convert Smart Kitchen's output format into the specific format each app expects.
- This makes the system extensible for future integrations with minimal changes to the core data pipeline.

---

