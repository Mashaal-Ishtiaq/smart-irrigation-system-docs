# Troubleshooting Guide – Smart Irrigation System

This guide helps developers, technicians, and operators identify and fix common issues.

---

## 1. Backend Issues

| Problem                  | Possible Cause                | Solution                                                        |
| ------------------------ | ----------------------------- | --------------------------------------------------------------- |
| Backend not starting     | Missing `.env` variables      | Check `.env` file and restart backend                           |
| Python dependency errors | `requirements.txt` outdated   | Run `pip3 install -r requirements.txt`                          |
| API returns 500          | Rule engine crash or DB error | Check logs: `docker logs irrigation-backend`                    |
| Port 8000 already in use | Another app running           | Change port in `docker-compose.yml` or stop conflicting service |

---

## 2. Database Issues

| Problem              | Possible Cause           | Solution                                                    |
| -------------------- | ------------------------ | ----------------------------------------------------------- |
| Cannot connect to DB | Service not running      | `docker-compose up -d db`                                   |
| Connection refused   | Wrong `DB_URL` in `.env` | Correct URL format: `postgresql://user:pass@db:5432/dbname` |
| Data missing         | Migration not run        | Ensure tables created, run DB setup scripts                 |

---

## 3. Rule Engine Issues

| Problem                   | Possible Cause           | Solution                                 |
| ------------------------- | ------------------------ | ---------------------------------------- |
| Irrigation never turns ON | Soil thresholds too high | Adjust `LOWER_LIMIT` in `rule_engine.py` |
| Irrigation always ON      | Thresholds too low       | Adjust `UPPER_LIMIT` in `rule_engine.py` |
| ET calculation incorrect  | PyETo misconfigured      | Validate inputs, check PyETo version     |
| Sensor data missing       | Gateway not sending      | Check ESP32 connectivity                 |

---

## 4. Sensor & IoT Issues

| Problem                  | Possible Cause    | Solution                        |
| ------------------------ | ----------------- | ------------------------------- |
| No data received         | ESP32 not powered | Verify power supply and network |
| Wrong sensor values      | Calibration issue | Recalibrate sensor or replace   |
| Rain sensor not detected | Wiring issue      | Check connections, verify GPIO  |

---

## 5. Swagger UI / API Docs Issues

| Problem             | Possible Cause          | Solution                          |
| ------------------- | ----------------------- | --------------------------------- |
| Swagger not loading | Volume path incorrect   | Check `docker-compose.yml` mounts |
| Wrong endpoints     | Outdated `openapi.yaml` | Update file and restart container |
| 404 error           | Wrong URL               | Use `http://<server-ip>:8081/`    |

---

## 6. Docker Issues

| Problem                           | Possible Cause          | Solution                                    |
| --------------------------------- | ----------------------- | ------------------------------------------- |
| Container crashes                 | Missing dependencies    | Rebuild: `docker-compose up --build -d`     |
| Port conflict                     | Another service running | Change mapped ports in `docker-compose.yml` |
| Containers not starting on reboot | Docker not enabled      | `sudo systemctl enable docker`              |

---

## 7. Logs & Debugging

* Backend: `docker logs -f irrigation-backend`
* DB: `docker logs -f irrigation-db`
* Rule Engine: check `engine.py` debug prints
* Network: `ping <ESP32-IP>` or `curl` API endpoints

---

## 8. Tips

* Always validate sensor values before sending to backend.
* Keep `.env` secure and updated.
* Use version control for `openapi.yaml` to track API changes.
* Perform back-testing for rule engine thresholds after major changes.
* Restart services in order: DB → Backend → Swagger UI.
