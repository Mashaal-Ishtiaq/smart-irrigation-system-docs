# Technicians FAQ – Smart Irrigation System

This FAQ is for technicians and operators. It explains the system in **simple, non-technical terms**.

---

## 1. What does the system do?

* Monitors soil moisture, temperature, humidity, rainfall, and water tank level.
* Automatically decides **when and how much to water the crops**.
* Sends data to a dashboard for monitoring and historical logs.

---

## 2. How do I know the system is working?

* Check the **web dashboard** or **mobile app** for real-time sensor readings.
* Pump status will be shown: **ON**, **OFF**, or **DELAY**.
* Alerts or warnings will appear if any sensor fails.

---

## 3. What if a sensor stops working?

* The system uses the **last valid reading** if a sensor fails.
* A faulty sensor must be **replaced or recalibrated**.
* Check the ESP32 gateway and wiring first.

---

## 4. Can I manually control irrigation?

* Yes, through the **dashboard** or **mobile app**.
* The rule engine will temporarily pause when manual control is used.

---

## 5. What do the ET and rule engine mean?

* **ET (Evapotranspiration):** measures how much water plants need.
* **Rule Engine:** decides **whether to water or not**, based on soil moisture, ET, and weather forecast.

---

## 6. What to do if the dashboard shows wrong readings?

* Refresh the dashboard.
* Check sensor connections.
* Verify the backend API is running: `http://<server-ip>/api/ping`.
* Check logs in Docker containers: `docker logs -f irrigation-backend`.

---

## 7. How do I update the system?

* Pull the latest code from GitHub.
* Restart services in this order:

  1. Database (`docker-compose up -d db`)
  2. Backend (`docker-compose up -d backend`)
  3. Swagger UI (`docker-compose up -d swagger`)

---

## 8. Who to contact if something is broken?

* If hardware (sensors, pump) → contact **IoT team**.
* If software (backend, dashboard) → contact **development team**.
* Always **document the problem** before escalating.

---

## 9. Daily Routine Checks

* Verify pump status and logs.
* Ensure all sensors are reporting correctly.
* Check water tank levels.
* Review system warnings and alerts.

---

## 10. Emergency Actions

* Turn off the pump manually if water overflows.
* Reboot the ESP32 gateway if sensors are unresponsive.
* Restart backend containers if the dashboard or rule engine stops responding.


## 11. How do I adjust soil moisture thresholds?

* Thresholds are defined in **rule-engine/engine.py** as constants: 
**LOWER_LIMIT = 30** and **UPPER_LIMIT = 70**. Edit these values and restart the backend.