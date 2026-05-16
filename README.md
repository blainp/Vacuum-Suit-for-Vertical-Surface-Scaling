# Vacuum Pump Wall Climbing Suit
This project features a fully custom, vacuum-powered, wearable system designed for scaling flat vertical walls. Developed over a 2.5-years, the system utilizes a centralized backpack-mounted dual Li-Po battery system to drive a quad-appendage vacuum pad array. By integrating an Arduino-based real-time pressure monitoring safety loop and cross-linked electronic solenoid valves, the suit establishes a reliable, redundant matrix of negative pressure that enables a natural, synchronized climbing gait while mitigating critical points of failure.

---

## Project Overview

<table>
  <tr>
    <td align="center" valign="top">
      <img width="350" src="https://github.com/user-attachments/assets/f7e0c13f-399c-461b-8a2c-9a949f581fa2" alt="System Diagram">
    </td>
    <td align="center" valign="top">
      <br><br><br>
      <img width="450" alt="3dFile" src="https://github.com/user-attachments/assets/fe27d63d-b476-471a-a850-adea5ee02db3" />
    </td>
  </tr>
</table>

### Design Evolution & Locomotion Model

This system was developed to solve the inherent safety and stability limitations discovered during initial structural testing of wearable pneumatic adhesion frameworks. 

> The first iteration relied on two independent all-in-one vacuum pads (one for each hand) paired with manual foot loops. This configuration created an absolute single point of failure where a sudden pressure loss on one pad caused immediate detachment, while requiring an unnatural, highly exhausting simultaneous hand-and-foot advance on a single side.

**By implementing a four-point contact array**, the second iteration migrates all primary electronics to an ergonomic backpack frame and redistributes suction force across four distinct mechanical pads—one for each appendage. This architectural pivot expands the total surface adhesion area, integrates two additional vacuum motors, and provides full systematic redundancy. 

**Natural Cross-Crawl Locomotion:** To allow fluid vertical movement, the pneumatic lines are cross-linked via electronic solenoids. Control buttons built directly into the arm-pad handgrips trigger the release of a specific arm pad *alongside* the diagonally opposite leg pad (e.g., releasing the left arm automatically releases the right leg). This allows the climber to safely alternate limbs while the remaining cross-diagonal pairs maintain continuous, unyielding adhesion to the wall surface.

### Hardware & Power Architecture

The suit's power bus relies on two 5000mAh high-amperage 12V LiPo batteries securely positioned at the apex of the backpack chassis. These cells feed a parallel power rail driving four high-output 12V -84KPA vacuum pump motors, with each motor dedicated to isolating a single suction channel.

**Pneumatic Control Loop:** Positioned inline between each vacuum pump and its corresponding pad is an electronic vacuum pressure sensor and a normally-closed solenoid valve. The analog sensor array continuously monitors the internal atmosphere of the pads, feeding telemetry data back to a central Arduino microcontroller that is powered cleanly via a 12V-to-5V step-down buck converter.

**Real-Time Safety Interface:** The microcontroller manages an active visual feedback safety loop using high-brightness LED clusters mounted directly onto the user's forward arm brackets:
- **Red LED (Insufficient Adhesion):** Indicated if vacuum pressure drops below the critical holding threshold ($\le -9\text{ PSI}$).
- **Green LED (Secure Adhesion):** Indicated only when *both* interdependent diagonal appendages (e.g., left arm and right leg) cross the safe holding threshold ($> -9\text{ PSI}$), providing unambiguous visual confirmation that the opposite diagonal pair can be safely detached and advanced.

### Mechanical & Wearable Construction

The vacuum pads are constructed from precision-milled, partially hollowed wood planks. The sealing interface uses a dual-layer strategy consisting of a robust commercial-grade rubber door gasket backed by an inner ring of high-density insulation foam. The entire structural assembly is injected and encapsulated with high-grade silicone to guarantee airtight seals against flat surfaces while maintaining a high coefficient of static friction to prevent vertical slippage.

**Ergonomic Integration:** 
- **Upper Body:** Arm pads are hard-mounted to heavy-duty wrist guards for stable forearm reinforcement, terminating in rugged metal hand grips housing the manual solenoid release buttons.
- **Lower Body:** Leg pads utilize modified high-impact hockey pad velcro mounting harnesses integrated with heavy-duty foot straps designed to absorb and shift the user's primary body weight away from the upper body. Recent design updates include extended high-density shin padding to project the lower pads outward, significantly improving mechanical leverage and wall contact angles.
- **Cable Management:** All high-current electrical wiring and flexible vacuum lines are bundled inside industrial corrugated tube shielding to prevent snagging or structural tearing. The lines are routed neatly along the shoulders and arms via low-profile mounting clips, utilizing heavy-duty electrical quick-connectors to facilitate rapid donning and doffing of the suit.

---

## Features

### Quad-Pad Redundant Adhesion
- Features an isolated four-channel pneumatic grid powered by independent -84KPA vacuum pumps.
- Ensures total system stability; loss of seal on a single channel will not compromise global weight-bearing integrity.

### Diagonal Solenoid Interlocking
- Cross-links electronic venting paths to support natural human cross-crawl climbing mechanics.
- Features mechanical handgrip micro-switches for tactile, precise control over atmospheric venting.

### Visual Telemetry Safety Matrix
- Monitors line pressure in real-time using an integrated Arduino microcontroller.
- Employs decoupled forearm status LEDs that prevent premature limb disengagement via localized sensor-interlocking rules.

---

## Repository Structure

```text
/Diagrams
    Electrical schematics, pneumatic routing plans, and system wiring layouts

/Documentation
    Design history, pressure analysis reports, and 2.5-year structural field logs

/Firmware
    Embedded C code for Arduino-based pressure tracking and LED logical safety matrix

/3D Models
    STL and Fusion 360 files for backpack electronics mounts and tubing line clips
```

---

## Bill of Materials (BOM)

| Component | Description | Function |
| :--- | :--- | :--- |
| Microcontroller | Arduino Development Board | Coordinates real-time sensor processing and safety indicator logic |
| Primary Power Source | 2x 5000mAh High-Amperage 12V LiPo Batteries | High-current power reservoir for the main motor/solenoid bus |
| Vacuum Pumps | 4x 12V -84KPA Pneumatic Pump Motors | Generates high-volume continuous negative pressure per pad |
| Solenoid Valves | 12V Normally-Closed Electronic Solenoids | Electronically isolates and releases pad vacuum on command |
| Pressure Sensors | Electronic Vacuum Analogs | Reads and outputs current pad-to-wall pressure states |
| Voltage Regulator | 12V-to-5V Step-Down Buck Converter | Drops main battery voltage to supply clean logic power to the Arduino |
| Mechanical Footwear | Integrated Hockey Pad Harnesses & Foot Straps | Shifts primary vertical load bearing to the lower muscle groups |

<p align="center">
<img width="1000" alt="image" src="https://github.com/user-attachments/assets/245cce53-bb9a-4866-85ff-58a84818fe8b" />
</p>

---

## Technical Specifications & Power Profile

The electrical and mechanical tolerances are calculated to sustain continuous high-load operational baselines during vertical ascents.

### Performance Profile

- **Target Run-Time:** `18+ Hours`
  - Total projected standby and operational cycle window derived from the dual 5000mAh LiPo configuration.
- **Adhesion Threshold:** `-9 PSI`
  - The strict software and physical cut-off limit required to change indicator status from Red to Green.

---

## Installation & Setup

### 1. Hardware Firmware Flash
* Open the source code found within `/Firmware` inside the Arduino IDE or your preferred editor.
* Flash the logic sketch to your target Arduino microchip.
* Open the Serial Monitor to verify baseline telemetry polling from the four analog pressure inputs.

### 2. Mechanical Calibration
* Power down the system and check that all normally-closed solenoids seal tightly without manual power.
* Ensure all quick-connectors are locked into place along the shirt routing clips.
* Apply power to the main 12V rails via the primary forearm toggles; monitor the status LEDs to ensure they boot to **Red** in open-air conditions.
* Press each pad against a flat test surface; verify that the indicators transition cleanly to **Green** as internal pressure passes the $-9\text{ PSI}$ operational floor.

---

## Media & Demonstration Logs

### Build Timelapse
*Documentation tracing the 2.5-year prototyping evolution, backpack layout creation, and structural pad fabrication phases.*

### Shortened Test Video
*A concise clip focusing on the system's active cross-crawl locomotion mechanism during successful vertical deployment (August 2024).*

### Full Test Video
*Uncut field-test records illustrating multi-point stability checks, automated LED status switching, and systematic detachment runs.*
