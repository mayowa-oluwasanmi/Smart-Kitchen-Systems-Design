# System Requirements for the Smart Kitchen

This document outlines the functional and non-functional requirements of the Smart Kitchen system, based on the proposed design. These requirements ensure that the system meets user needs, supports intended functionalities, and remains scalable, reliable, and usable in real-world kitchen environments.

---

## 1. Functional Requirements

These are core behaviors and capabilities the Smart Kitchen system **must** deliver:

### 1.1. Food Detection and Measurement
- The system must detect and identify food items placed on the counter or stovetop.
- The system must measure the weight of food items in grams using load cell sensors.
- The system must capture visual input (via CMOS sensor) or scan barcodes to classify food items.

### 1.2. Nutritional Data Retrieval
- The system must retrieve nutritional information (e.g., calories, protein, carbs, fats, sodium, fiber) from a local or cloud-based Oracle database.
- Nutritional data must be tied to specific food types identified by barcode or image recognition.

### 1.3. Real-Time Feedback
- The system must provide real-time dietary feedback to users via the LCD touchscreen tablet.
- The tablet must show calorie count and macronutrient profile as food is placed on the sensors.

### 1.4. Logging and Historical Tracking
- The system must log daily and weekly food intake.
- Users must be able to view previous meals through the tablet interface.

### 1.5. Recommender System
- When applicable, the system must suggest low-calorie food alternatives (< 100 kcal per 100g).
- Recommendations must be tailored to user-defined goals (e.g., weight loss, nutrient focus).

### 1.6. Integration with External Apps
- The system must allow for synchronisation with nutrition and fitness apps (e.g., MyFitnessPal).
- Exported data must include total calorie intake, macronutrients, and meal breakdowns.

---

## 2. Non-Functional Requirements

These are quality attributes the system must uphold:

### 2.1. Usability
- The interface must be intuitive and accessible, suitable for users with varying tech literacy.
- Data visualization must be clear, concise, and color-coded where possible.

### 2.2. Performance
- The system must deliver real-time feedback (<1s delay) after a food item is placed.
- Sensor data must be processed and displayed without noticeable lag.

### 2.3. Reliability
- The system must operate consistently over long periods (daily kitchen use).
- In case of sensor error or barcode failure, fallback measures (e.g., manual entry) should be supported.

### 2.4. Accuracy
- Weight sensors must be accurate within ±2 grams.
- Nutritional output must align with verified food databases (e.g., USDA, manufacturer barcode info).

### 2.5. Environmental Robustness
- All hardware (sensors, tablet, microcontroller) must be water-resistant and heat-tolerant.
- The CMOS sensor must include dedicated LED lighting to ensure image quality under variable lighting.

### 2.6. Scalability
- The system must support additional sensors and new modules (e.g., fridge integration).
- The backend should be expandable to handle larger datasets or user bases.

### 2.7. Maintainability
- Sensor and software modules must be modular for easy replacement or upgrade.
- Software updates must be deliverable over Wi-Fi without requiring hardware modification.

---

## 3. Hardware Requirements

| Component                    | Requirement                                            |
|-----------------------------|--------------------------------------------------------|
| Load Cell                   | 1kg capacity, compatible with HX711 module             |
| CMOS Sensor                 | Moderate resolution with white LED for visibility      |
| Barcode Scanner             | Capable of decoding standard food packaging barcodes   |
| Microcontroller             | Wi-Fi enabled (e.g., ESP32), compatible with sensors   |
| Display                     | Touchscreen LCD, moisture and heat-resistant           |
| Wi-Fi Module                | 802.11ac standard                                      |
| Power Supply                | Standard kitchen-safe power adapter or battery backup  |

---

## 4. Software Requirements

| Component                    | Requirement                                            |
|-----------------------------|--------------------------------------------------------|
| Database                    | Oracle DB for structured food/nutrient storage         |
| Data Format                 | JSON for backend–frontend communication                |
| Communication Protocol      | HTTP for sensor-controller-server communication       |
| Backend                     | Python (Flask/Django) or Node.js (Express) suggested  |
| Third-Party Integration     | Support for nutrition and fitness APIs                 |

---

## 5. Assumptions and Constraints

- Users place only one food item at a time on the counter/stovetop to ensure accurate measurement.
- The kitchen must be reasonably well-lit for effective CMOS imaging.
- System assumes the user has basic nutritional literacy or prior experience with food tracking.
- System must operate offline with delayed sync in case of connectivity loss.

---

## 6. Future Considerations

- Use of computer vision models (e.g., YOLO, MobileNet) for ingredient detection.
- Implementation of educational tutorials or interactive learning for nutritional literacy.
- Fridge/pantry inventory integration via RFID or IoT modules.

---

## Conclusion

These requirements define the scope and expectations of the Smart Kitchen system. They support the project’s goal of reducing user burden, increasing accuracy in food logging, and empowering users to make informed dietary decisions with minimal intrusion or complexity.
