**Compact ESP32 Development Board with USB-C, LiPo Charging, and IMU.**

` `**Power Management Design Decisions**

**Power Sources & Regulation**

- **USB-C Interface:** Provides primary 5V power supply.
- **LiPo Battery (TP4056 Module):** Secondary power source for portability.
- **Voltage Regulation:**
  - **AMS1117-3.3V:** Converts 5V from USB or ~4.2V from LiPo to 3.3V for ESP32 and peripherals.
  - **Bypass Capacitors:** 10µF capacitors placed at input/output of AMS1117 for stability.

**Power Path & Switching**

- **Schottky Diode:** Prevents reverse current flow between USB and battery.
- **Automatic Switching:** The TP4056 module allows seamless transition between USB power and battery power.
- **Battery Voltage Monitoring:** Voltage divider circuit connected to ESP32 ADC for real-time monitoring.

**Thermal Considerations**

- **Copper Pouring:** Used around AMS1117 for heat dissipation.
- **Component Placement:** AMS1117 positioned near the power input with adequate spacing to reduce heat buildup.
-----
**2. Debugging Features**

**Serial Communication for Debugging**

- **CH340G USB-to-UART Converter:** Facilitates USB serial communication.
- **Connections:**
  - **ESP32 TX → CH340G RX**
  - **ESP32 RX → CH340G TX**
  - **ESP32 IO0 → CH340G DTR** (for automatic boot mode selection)
  - **ESP32 EN (Reset) → CH340G RTS** (for automatic reset)

**Boot & Reset Controls**

- **Reset Button:** Connected to ESP32 EN pin for manual reset.
- **Boot Button:** Connected to ESP32 IO0 for manual boot mode selection.
- **Pull-up Resistors:** 10kΩ resistors on EN and IO0 for stability.

**Status Indicators**

- **Power LED:** Indicates if board is powered.
- **Charge Indicator LEDs:** Shows charging status via TP4056 module.
- **ESP32 Boot Mode LED:** Flashes when entering programming mode.

**Test Points & Expansion**

- **Exposed Test Points:** For 3.3V, GND, TX, RX, SCL, SDA, and other key signals.
- **GPIO Headers:** Allow additional peripherals to be connected.
-----
**3. PCB Layout Considerations**

**Power & Ground Planes**

- **Thicker Traces:** Used for high-current paths (~0.5mm width).
- **Dedicated Ground Plane:** Reduces noise and improves signal integrity.

**Component Placement for Debugging**

- **USB & CH340G:** Placed near board edge for easy USB access.
- **Test Points & Headers:** Clearly labelled and spaced for easy probing.

**Thermal & Noise Management**

- **AMS1117 Heat Dissipation:** Thermal vias and copper pours help manage heat.
- **Decoupling Capacitors:** Placed near power pins of ESP32 and MPU6050.
-----
**Conclusion**

This design ensures reliable power management with seamless USB/LiPo switching and efficient debugging features, making development and troubleshooting easier. Proper PCB layout techniques enhance stability and performance.

