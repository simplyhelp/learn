
## Best Practices for Accurate GNSS Data Collection with Consumer Devices

**Applies to:** Smartphones, tablets, handheld GPS units, drones (non-corrected GNSS)

---

# Key practices for Maximizing Location Precision and Accuracy

---

## 1. Get a Clear View of the Sky

* Use in **open areas**, away from buildings and tall trees.
* Avoid dense canopy, walls, vehicles, or anything blocking the sky.
* Keep the device **away from your body and metal surfaces**.
* Once a lock is established (see soaking below) moving closer to these objects is fine, but the accuracy+precision may degrade

---

## 2. Soak the Signal Before Recording

* **Wait 2–5 minutes** at a new location before collecting data.
* Moving <1km is fine to collect, it's moving significantly away that requires soaking. 
* This allows the device to fully connect to available satellites.

---

### 3. Use Point Averaging

* Stay completely **still** for 30–60 seconds while collecting a point.
* Use **averaging tools** in your app or GPS if available.
* No tool? Take multiple points and average them manually.

---

### 4. Enable Multi-Constellation GNSS

* Use devices that support **NavStar/GPS + GLONASS + Galileo + BeiDou**.
* Ideal combination is **GPS/NavStar + Galileo**
* On phones, enable **High Accuracy Mode** (Android) or Location Services (iOS).

---

### 5. Monitor Satellite Geometry (HDOP/PDOP)

* Collect data when **HDOP < 1.5** for better precision.
* Avoid collecting when HDOP > 2.5.
* Use apps that show HDOP (e.g., GPS Status, Field Maps, Locus).
* https://www.gnssplanning.com/ can be used to plan in the future or see past possible signals

---

### 6. Don’t Move While Recording 🚷

* Movement = position jumps.
* Use a tripod, or hold the device steady at chest or eye level.
* If recording a line, move more slowly or be prepared to edit the line later

---

### ⚠️ 7. Minimize Interference

* Keep the device **away from large metal objects, electronics, radios, and terrain or large rocks**.
* Metal and glass surfaces can reflect signals (multipath error)
* Blocking signal line of sight

---

### 8. Plan for Good Timing

* Satellite alignment changes during the day.
* If possible, collect data during times of **low HDOP**.
* Avoid collection during **solar storms** (check NOAA space weather).

For more info or to get an HDOP planning app, try:

* **GPS Status & Toolbox** (Android)
* **GNSS View** (iOS)
* **Trimble GNSS Planning Online**


| Factor                 | Recommendation                               | Benefit                                         |
| ---------------------- | -------------------------------------------- | ----------------------------------------------- |
| **Line of Sight**      | Open sky, away from buildings/canopy         | Better satellite visibility                     |
| **Soaking**            | Wait 2–5 min before capture                  | More stable satellite lock                      |
| **Averaging**          | Stay still 30–60 sec, use averaging tool     | Reduces random jitter                           |
| **Satellite Geometry** | Use apps to monitor HDOP < 1.5               | Higher positional certainty                     |
| **Constellations**     | Enable GPS + GLONASS + Galileo               | More satellites = better fixes                  |
| **Motion**             | Don’t move during data collection            | Increases precision                             |
| **Interference**       | Avoid metal/electronics, hold away from body | Reduced signal distortion                       |
| **External Antenna**   | Optional for handheld or Bluetooth GNSS      | Enhanced reception, better multipath resistance |
| **Time of Day**        | Plan for low HDOP periods                    | Better accuracy from better geometry            |
| **A-GNSS Mode**        | Disable for satellite-only tests             | Pure GNSS performance measurement               |
