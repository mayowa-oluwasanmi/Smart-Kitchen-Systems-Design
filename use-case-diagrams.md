# Detailed Use Cases for Smart Kitchen System

---

## Use Case 1: Measure Food Intake

**Use Case ID:** UC-01  
**Actors:** User, Smart Kitchen System  
**Preconditions:**  
- Smart Kitchen system is operational.  
- Food items are ready to be prepared or consumed.  
- Sensors (weight, barcode scanner, CMOS camera) are active and calibrated.  

**Basic Flow:**  
1. User places a single food item on the kitchen counter or stovetop.  
2. Load cell weight sensors measure the weight of the item.  
3. Barcode scanner scans the packaging if the item is prepackaged.  
4. CMOS sensor captures an image if the item is fresh or unpackaged.  
5. System processes the data to identify the food type and weight.  
6. Nutritional information (calories, macronutrients) is retrieved from the backend database.  
7. Data is logged and made ready for feedback display.

**Alternate Flows:**  
- 3a. If barcode cannot be read, system prompts user to manually input or retry.  
- 4a. If CMOS image is unclear (poor lighting), system requests user to improve lighting or reposition item.  
- 1a. If multiple items placed simultaneously, system may fail to differentiate (known limitation).

**Postconditions:**  
- Food intake data is accurately recorded in the system database.  
- Nutritional information is ready to be displayed.

---

## Use Case 2: Provide Real-Time Nutritional Feedback

**Use Case ID:** UC-02  
**Actors:** User, Smart Kitchen System  
**Preconditions:**  
- Food intake measurement has been successfully completed.  
- LCD tablet interface is active and connected to the system.  

**Basic Flow:**  
1. System calculates the calorie count and macronutrient profile based on measured data.  
2. Real-time nutritional data is displayed on the LCD tablet.  
3. User views calorie count, protein, carbs, fats, sodium, potassium, iron, fiber, etc.  
4. User adjusts meal preparation or ingredients based on feedback if desired.

**Alternate Flows:**  
- 2a. If the tablet is not responsive, system attempts to resend data or alerts user.  
- 4a. User ignores feedback (system does not enforce changes, just provides information).

**Postconditions:**  
- User is informed about the nutritional content of current meal preparation.  
- Data is logged for future reference.

---

## Use Case 3: Synchronize with Nutrition and Fitness Apps

**Use Case ID:** UC-03  
**Actors:** Smart Kitchen System, Nutrition Tracking Apps, Fitness Trackers  
**Preconditions:**  
- User has authorized integration with third-party apps.  
- Network (WiFi 802.11ac) connection is stable.  

**Basic Flow:**  
1. Smart Kitchen system aggregates daily nutritional intake data.  
2. Data is formatted into JSON and securely transmitted via HTTP to connected apps.  
3. Nutrition and fitness apps update user profiles with new intake data.  
4. User can view combined dietary logs from home and external meals.

**Alternate Flows:**  
- 2a. If network connection fails, data is queued and sent when connection is restored.  
- 3a. If authorization is revoked, synchronization stops and user is notified.

**Postconditions:**  
- User's dietary data is synchronized across multiple platforms for comprehensive tracking.

---

## Use Case 4: Recommend Low-Calorie Food Alternatives

**Use Case ID:** UC-04  
**Actors:** User, Smart Kitchen System  
**Preconditions:**  
- User’s nutritional goals and preferences are set in the system.  
- Food intake data is available for analysis.  

**Basic Flow:**  
1. System analyses current meal’s nutritional content.  
2. System queries database for low-calorie alternatives (<100 kcal/100g) matching the type of ingredient used.  
3. Recommended alternatives are displayed on the LCD tablet with nutritional benefits.  
4. User reviews recommendations and chooses to accept or ignore.  

**Alternate Flows:**  
- 3a. If no suitable alternative found, system informs user accordingly.  
- 4a. User rejects all recommendations; system logs decision but does not enforce changes.

**Postconditions:**  
- User receives guidance to support healthier eating choices.  
- Recommendations help inform user decisions without being intrusive.

---

## Use Case 5: Display Historical Dietary Logs

**Use Case ID:** UC-05  
**Actors:** User, Smart Kitchen System  
**Preconditions:**  
- The system has logged dietary intake data over time.  
- LCD tablet is active and connected.  

**Basic Flow:**  
1. User selects the ‘Previous Log’ option on the tablet interface.  
2. System retrieves historical dietary data (daily/weekly summaries) from the database.  
3. Nutritional intake summaries are displayed clearly with calories and macronutrient breakdown.  
4. User reviews past intake to inform future meal choices.

**Alternate Flows:**  
- 2a. If no previous data exists, system informs the user.  
- 3a. If display malfunctions, system attempts to reload or alerts user.

**Postconditions:**  
- User gains insight into past eating habits.  
- Supports self-monitoring and dietary awareness over time.

---

![Screenshot_5-6-2025_183143_](https://github.com/user-attachments/assets/5a1da880-22d1-4f77-bbd5-3b8cd9be50e2)
