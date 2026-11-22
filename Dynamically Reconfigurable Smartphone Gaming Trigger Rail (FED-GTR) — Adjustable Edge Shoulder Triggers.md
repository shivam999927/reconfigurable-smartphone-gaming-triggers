# Full-Edge Dynamically Reconfigurable Gaming Trigger Rail (FED-GTR)

**Document Type:** Defensive Technical Disclosure / Prior Art Publication  
**License:** CC0 1.0 Universal (Public Domain Dedication) — Free for public and commercial implementation without patent restriction.

---

## 1. Abstract
A hardware-software architecture for mobile devices (specifically gaming smartphones) that replaces fixed-position shoulder triggers with a continuous, full-length touch/pressure-sensitive sensor array integrated along one or more lateral edges of the device chassis. Through system-level software, the user dynamically defines, positions, resizes, and enables between **1 and 4 independent virtual trigger zones** anywhere along the continuous sensor rail, while all remaining unselected regions of the rail are programmatically deactivated ("dead-zoned") at the firmware/driver level to eliminate accidental palm and grip inputs.

---

## 2. Problem Statement
Current gaming smartphones rely on either:
1. **Fixed mechanical/ultrasonic shoulder buttons** positioned strictly near the top-left and top-right corners in landscape orientation, which fail to accommodate varying hand sizes, finger lengths, and multi-finger grip styles (e.g., 3-finger, 4-finger, or 6-finger claw grips).
2. **Continuous edge-touch displays** that suffer from severe accidental activation caused by the user's palms and supporting fingers gripping the device rails during intense gameplay.

---

## 3. System Architecture & Hardware Design

### 3.1 Continuous Side-Rail Sensor Array
Instead of discrete sensor pads at the corners, the device embeds a continuous linear array of **N** discrete sensing nodes (`S_0` to `S_n`) spanning 80%–100% of the top/side frame length in landscape orientation. 

Supported sensor modalities include:
* **Segmented Capacitive Touch Array:** High-density copper/ITO electrode strips with individual channel addressing.
* **Piezoelectric / Strain-Gauge Force Array:** Micro-force transducers capable of distinguishing intentional press force (`F_trigger`) from passive resting grip pressure (`F_grip`).
* **Multi-Transducer Ultrasonic Array:** Linearly arranged ultrasonic emitters/receivers measuring acoustic impedance shifts along the metal/glass frame.

```text
+-----------------------------------------------------------------------+
| [S0][S1][S2][S3][S4][S5][S6][S7][S8][S9][S10][S11][S12][S13][S14][S15]|  <-- Continuous Full-Edge Sensor Rail
+-----------------------------------------------------------------------+
|                                                                       |
|                                                                       |
|                         SMARTPHONE DISPLAY                            |
|                       (Landscape Orientation)                         |
|                                                                       |
|                                                                       |
+-----------------------------------------------------------------------+
4. Software Control Layer & User Interface
4.1 Dynamic Trigger Placement UI
  A system-level overlay (accessible via the gaming dashboard) renders a visual ruler along the physical edge of the screen to the sensor   rail underneath:

  Add/Remove Triggers: Users toggle 1, 2, 3, or 4 independent trigger slots per edge.

  Drag-to-Position: Users slide each virtual trigger icon along the screen edge to align directly beneath their natural resting finger positions.

  Resize Width: Users pinch or drag trigger boundaries to make a trigger zone narrow (for rapid precision taps) or wide (for ergonomic comfort).

  Per-Trigger Mapping: Each active zone maps independently to an on-screen (x, y) touch coordinate, macro sequence, or hardware button code.
+-----------------------------------------------------------------------+
|      [ T1: Aim ]                  [ T2: Fire ]       [ T3: Crouch ]   |  <-- On-Screen Visual Overlay
+-----------------------------------------------------------------------+
|  |----Zone 1----|                |---Zone 2---|     |----Zone 3----|  |
|                                                                       |
|          (O)                                                          |
|       Move Stick                                         [Jump]       |
|                                                                       |
+-----------------------------------------------------------------------+
5. Optional Multi-Stage & Feedback Enhancements
  Dual-Threshold Force Sensing: If implemented with piezoelectric/pressure sensors, each custom zone supports two actuation thresholds—a light press (Action A) and a deep press (Action B).

  Localized Haptic Confirmation: Upon actuation of Zone i, a linear resonant actuator (LRA) triggers a crisp, short-duration haptic pulse to simulate a mechanical micro-switch click.

  Sub-Surface Edge LED Indicators: Micro-LEDs embedded beneath the side rail illuminate only under the active [X_start, X_end] intervals when Game Mode is enabled, providing immediate visual alignment without looking at settings.
6. Author's Addendum & Scope Clarifications

To prevent narrow legal workarounds or partial-implementation patents, the following clarifications apply to the entire concept described above:

* **Arbitrary Number of Triggers (`N ≥ 1`):** While 1 to 4 triggers represent common ergonomic presets, the system is not limited to 4 triggers. The software and firmware architecture covers **any integer number of simultaneous active trigger zones (1, 2, 3, 4, 5, 6, or more)** up to the physical resolution limit of the underlying sensor array.
* **Flexible Coverage Area & Strip Geometry (`>0% to 100%`):** The sensor array is not restricted to covering 80%–100% of the chassis edge. This disclosure covers **any partial or full-length continuous sensor strip or thin sensing band** (covering anywhere from a fraction of the edge up to 100% of one or multiple edges, including top, bottom, left, right, or curved frame bezels) where the user can dynamically place and relocate active trigger zones while masking/deactivating the unused portions of that strip.
* **Core Principle:** Any mobile device that provides a continuous or multi-node side sensing region—regardless of strip thickness or percentage of frame coverage—and uses software to dynamically define where virtual triggers are active while suppressing accidental touches in the remaining unused areas falls within the scope of this public disclosure.