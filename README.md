# Vacuum Pump Wall Climbing Suit
This project features a fully custom, vacuum-powered, wearable system designed for scaling flat vertical walls utilizing a centralized, backpack-mounted dual Li-Po battery architecture to drive a quad-appendage vacuum pad array. By integrating cross-linked electronic solenoid valves, the suit provides a reliable and redundant matrix where 2 contralateral appendages are always connected to the wall, enabling a natural and synchronized climbing gait. Additionally, an Arduino-based real-time pressure monitoring and seal integrity feedback loop was integrated to alert the user to incomplete or failed vacuum seals, preventing false assumptions of secure attachment and reducing the risk of injury.

---

<p align="center">
  <a href="https://www.youtube.com/watch?v=eWJluZnBhK0">
    <img src="https://github.com/user-attachments/assets/a2f6d8ae-4f06-4bfa-942c-a9f9f2d7124c" width="800" />  
  </a>
  <br>
  FULL TEST VIDEO
</p>



---

## Design Evolution 

The first iteration of this project relied on two independent all-in-one vacuum pads (one for each hand) paired with manual foot loops. This configuration created an absolute single point of failure where a sudden pressure loss on one pad caused the immediate detachment of the whole system. Additionally, this iteration required an unnatural and highly exhausting simultaneous hand-and-foot advance on a single side, as a user had to lift a pad and foot together.

<p align="center">
<img height="400" alt="image" src="https://github.com/user-attachments/assets/deb7f468-12f8-4b31-bcef-91a5b945b86f" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/483c195e-9417-4fa7-9899-63320096bbad" />
</p>





**By implementing a four-point contact array**, the second iteration migrates all primary electronics to an ergonomic backpack frame and redistributes suction force across four distinct mechanical pads, one for each appendage. This architectural pivot expands the total surface adhesion area, integrates two additional vacuum motors, increasing the overal suction force, and provides systematic redundancy. 

<p align="center">

</p>



**Natural Movement Gait** To improve vertical movement fluidity the pneumatic lines were cross-linked via electronic solenoids. Control buttons built directly into the arm-pad handgrips trigger the release of a specific arm pad *alongside* the diagonally opposite leg pad (e.g., releasing the left arm automatically releases the right leg). This allows the climber to safely alternate limbs while the remaining cross-diagonal pairs maintain continuous adhesion to the wall surface. Essentially, the improved climbing style of the second iteration resembles that of Spiderman, switching between pairs of contralatteral appendages, in contrast to the first iteration, which had the user shifting their entire body left and right to climb.

### Hardware & Power Architecture

The suit's power system relies on two 5000mAh high-amperage 12V LiPo batteries securely mounted at the top of the backpack frame. These cells feed a parallel power rail driving four high-output 12V -84KPA vacuum pump motors, with each motor dedicated to isolating a single suction channel.

<p align="center">
<img width="800" alt="ClimbingSuitWiringDiagram" src="https://github.com/user-attachments/assets/0e5f03dd-c619-4739-a471-513085bc9557" />
</p>

**Pneumatic Control Loop:** Positioned inline between each vacuum pump and its corresponding pad is an electronic vacuum pressure sensor and a normally-closed solenoid valve. The analog sensor array continuously monitors the internal atmosphere of the pads, feeding telemetry data back to a central Arduino microcontroller which is powered by a 12V to 5V XL6009 buck converter.

**Real-Time Safety Interface:** The microcontroller manages an active visual feedback safety loop using high-brightness LED clusters mounted directly onto the user's forward arm brackets:
- **Red LED (Insufficient Adhesion):** Indicated if vacuum pressure drops below the critical holding threshold ($\le -9\text{ PSI}$).
- **Green LED (Secure Adhesion):** Indicated only when *both* interdependent diagonal appendages (e.g., left arm and right leg) cross the safe holding threshold ($> -9\text{ PSI}$), providing unambiguous visual confirmation that the opposite diagonal pair can be safely detached and advanced.

 

<p align="center">
<img width="1236" height="1032" alt="image" src="https://github.com/user-attachments/assets/63893b26-d502-406d-bf77-20e505984326" />
</p>

## Safety Threshold Value Calculation
The vacuum cutoff safety threshold of **−9 psi (≈ −62 kPa)** was derived from required load support conditions under conservative friction and safety assumptions.

### Design Assumptions

- **User weight:** 170 lb  
- **Coefficient of friction (μ):** 0.5  
  - Expected range: 0.4–1.0 depending on surface condition and seal compliance  
- **Safety factor:** 2×  
- **Load case:** alternating support via one arm pad + one leg pad

### Required Support Force

Applying the safety factor: 170 lb would become 340 lb of equivalent design load

Accounting for friction-limited adhesion: F_normal = 340 / 0.5 = 680 lbf (directly vertical application)

### Contact Area Model

Pad contact areas:
- Arm pad: 9 × 4 in = 36 in²  
- Leg pad: 10 × 6 in = 60 in²  
- Total active area per support phase: 96 in²  

### Vacuum Pressure Requirement

Required pressure differential: P = 680 lbf / 96 in² ≈ 7.1 psi

### Design Margin and Selection
To account for real-world inefficiencies including:
- imperfect seal conformity  
- transient leakage during gait transitions  
- non-uniform pressure distribution  
- dynamic loading effects  

a conservative design margin was applied, resulting in the operational threshold:

**Vacuum cutoff threshold: −9 psi (≈ −62 kPa gauge)**

### System Compatibility

The selected vacuum generation system is rated for:

**Maximum vacuum:** −85 kPa

As the selected vacuum pump motors were rated for -85kPa, this provided sufficient operational headroom above the cutoff threshold to accommodate slight losses while maintaining safe functional operation.

### Mechanical & Wearable Construction

The vacuum pads were constructed from milled and partially hollowed wood planks. The sealing interface utilizes a dual layer system, consisting of a standard rubber door gasket backed by an inner ring of high-density insulation foam. This entire seal assembly was then injected and encapsulated with silicone to construct airtight seals against flat surfaces while maintaining a high coefficient of static friction.

<p align="center">
<img width="689" height="528" alt="tocrop" src="https://github.com/user-attachments/assets/c368565b-4fd9-4188-afcc-bd5474aa620c" />
</p>



**Ergonomic Integration:** 
- **Upper Body:** Arm pads are hard-mounted to heavy-duty wrist guards for stable forearm reinforcement, terminating in rugged metal hand grips housing the manual solenoid release buttons.
- **Lower Body:** Leg pads utilize modified hockey pad velcro mounting harnesses integrated with heavy-duty foot straps designed to absorb and shift the user's primary body weight away from the upper body. Recent design updates include extended high-density shin padding to project the lower pads outward, improving mechanical leverage and wall contact angles.
- **Cable Management:** All  electrical wiring and flexible vacuum lines are bundled inside corrugated tube shielding to prevent snagging or structural tearing. These tubes are routed along the shoulders and arms via mounting clips, utilizing electrical quick-connectors to facilitate rapid wearing and removal of the suit.

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

---
<p align="center">
  <a href="https://www.youtube.com/watch?v=LduNefReZHM">
    <img width="600" alt="TimelapsePic" src="https://github.com/user-attachments/assets/0a8d7160-966c-421d-9c1b-d69f7c94c3f8" />
  </a>
  <br>
  BUILD TIMELAPSE
</p>

<p align="center">
  <a href="https://www.youtube.com/watch?v=KHBrrZLr4q0">
   <img width="600" alt="ShortenedPic" src="https://github.com/user-attachments/assets/d98de2ad-8e97-44f6-b6da-eb869c73b86d" />
  </a>
  <br>
 SHORTENED TEST VIDEO
</p>


