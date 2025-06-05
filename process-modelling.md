# Process Modelling for the Smart Kitchen System

This document describes the main processes and workflows that underpin the Smart Kitchen system. It explains how data flows between components and how user interactions drive system behavior. The purpose is to provide a clear understanding of the system’s dynamic behavior for development and validation.

---

## 1. Overview

The Smart Kitchen automates food intake tracking by combining sensor data (weight and images), barcode scanning, and nutritional database queries. It delivers real-time feedback and historical logs through an LCD touchscreen interface while syncing data with external nutrition apps.

---

## 2. Key Processes

### 2.1 Food Item Detection and Identification

**Actors:** User, Weight Sensor, CMOS Sensor, Barcode Scanner, Microcontroller  
**Description:**  
- The user places a single food item on the kitchen counter or stovetop.  
- Load cell sensors measure the item's weight.  
- The CMOS sensor captures an image of the food item for classification (fresh/whole foods).  
- The barcode scanner scans packaging to identify prepackaged or processed foods.  
- The microcontroller collects sensor inputs and consolidates data for processing.

**Flow:**  
1. User places item → sensors trigger data capture.  
2. Microcontroller reads weight from load cell.  
3. CMOS sensor takes image; image processed for identification or stored for later classification.  
4. Barcode scanner attempts to read barcode if packaging is present.  
5. Data is encoded in JSON format and sent over Wi-Fi (802.11ac) to the backend server.

---

### 2.2 Nutritional Data Retrieval and Analysis

**Actors:** Backend Server, Oracle Database, Microcontroller  
**Description:**  
- The backend server receives sensor data from the microcontroller.  
- Using barcode or image classification, the server queries the Oracle database for nutritional information.  
- Nutritional values (calories, macronutrients, micronutrients) per gram are extracted.  
- Real-time calculation multiplies per-gram data by measured weight to obtain meal-specific nutrient counts.

**Flow:**  
1. Backend receives JSON payload with item ID, image data, and weight.  
2. Query Oracle DB for matching nutritional profile.  
3. Calculate total nutrients for the measured weight.  
4. Return data to microcontroller/display device.

---

### 2.3 User Feedback and Visualization

**Actors:** User, LCD Touchscreen Tablet  
**Description:**  
- The system displays real-time nutritional feedback on the tablet as the user adds ingredients.  
- Displays calorie count, macronutrient breakdown (protein, fats, carbs, sodium, fiber, etc.).  
- Shows daily calorie totals and compares against user’s TDEE (Total Daily Energy Expenditure).  
- Allows access to previous logs and recommended low-calorie alternatives.  
- Users can interact with the tablet to set goals or explore past intake.

**Flow:**  
1. Microcontroller sends nutritional analysis to tablet.  
2. Tablet updates UI with real-time nutrient information.  
3. User views info and optionally selects recommended alternatives.  
4. User navigates to past logs or settings as needed.

---

### 2.4 Data Synchronization with External Applications

**Actors:** Smart Kitchen Backend, Third-Party Nutrition/Fitness Apps  
**Description:**  
- Aggregated daily intake data is synced with nutrition apps (e.g., MyFitnessPal).  
- Enables consolidated food logging for meals consumed outside the kitchen environment.

**Flow:**  
1. Backend formats daily intake data into API-compatible format.  
2. Data transmitted over HTTP(s) to third-party app API.  
3. Third-party app integrates Smart Kitchen data alongside user-entered meals.  
4. User accesses comprehensive intake overview in external app.

---

### 2.5 Error Handling and User Input Override

**Actors:** User, Microcontroller, LCD Tablet  
**Description:**  
- If sensor data is unclear or missing (e.g., barcode not detected, image blurry), the system prompts the user for manual input.  
- User can manually enter or correct food item details or quantities.  
- The system updates logs and nutritional calculations accordingly.

**Flow:**  
1. Sensor failure detected → prompt displayed on tablet.  
2. User inputs item details or selects from suggestions.  
3. System updates backend and continues normal operation.

---

## 3. Process Flow Diagram (Summary)

```plaintext
User places item
      ↓
Sensors measure weight, scan barcode, capture image
      ↓
Microcontroller collects data → sends JSON payload over Wi-Fi
      ↓
Backend Server queries Oracle DB for nutrition data
      ↓
Backend calculates nutritional values based on weight
      ↓
Nutritional data sent to LCD Tablet for display
      ↓
User views real-time feedback & interacts with system
      ↓
Data synced with external apps for comprehensive tracking
