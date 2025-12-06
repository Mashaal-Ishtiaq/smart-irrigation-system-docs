# Risks & Mitigation – Smart Irrigation System

This document lists potential risks in the system and suggested mitigation strategies.

---

## 1. ET Calculator Accuracy

**Risk:**
Evapotranspiration (ET) calculations may be inaccurate due to sensor errors or incorrect parameters.

**Mitigation:**

* Use the **PyETo library** as reference for calculations.
* Validate ET values against published agricultural data.
* Perform periodic calibration of temperature, humidity, and solar sensors.
* Log ET results and compare with historical trends for anomaly detection.

---

## 2. Rule Engine Behavior

**Risk:**
The rule engine may be too **conservative** (watering too little) or **aggressive** (watering too much).

**Mitigation:**

* Test rule engine using **historical sensor data**.
* Adjust thresholds (soil moisture limits, ET levels) iteratively based on testing.
* Implement fallback logic for missing or invalid sensor data.
* Document and log each decision for auditing and analysis.

---

## 3. Sensor Failures or Missing Data

**Risk:**
Faulty or disconnected sensors can lead to incorrect irrigation decisions.

**Mitigation:**

* Implement **last-known-valid readings** in the rule engine.
* Send alerts to dashboard when sensors are unresponsive.
* Regularly check and maintain IoT sensors and wiring.

---

## 4. Backend API or Database Downtime

**Risk:**
If the backend API or database is unavailable, the system cannot process sensor data or make decisions.

**Mitigation:**

* Use **Docker restart policies** to auto-restart services.
* Monitor containers using logs and alerts.
* Ensure backup database and replication if needed.
* Schedule maintenance during low irrigation periods.

---

## 5. Weather Forecast Unavailability

**Risk:**
Weather API failure may affect irrigation decisions (e.g., rain expected).

**Mitigation:**

* Rule engine can operate **without weather forecast** using soil moisture and ET only.
* Retry weather API calls multiple times before fallback.
* Log missing forecast events for review.

---

## 6. Human Error

**Risk:**
Manual intervention may override system settings incorrectly.

**Mitigation:**

* Include confirmation prompts for manual overrides.
* Keep detailed logs of all manual actions.
* Provide clear guidance in **Technician FAQ** for safe operations.

