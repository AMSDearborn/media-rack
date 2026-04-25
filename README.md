# 📡 AMS Media & IT Rack Architecture Documentation

This document serves as the official reference guide for the AMS Media and IT Committee's 15U wall-mounted rack. It outlines the purpose of the interactive web visualizer, the physical unit-by-unit hardware layout, and a deep-dive into the network patch panel routing.

---

## 🖥️ Part 1: The Interactive Web Visualizer

To assist volunteers and committee members in understanding this complex infrastructure, a single-file interactive web application (`rack-diagram.html`) has been developed. 

### Key Features of the Web App:
*   **Interactive 15U Interface:** Click on any unit in the rack to view its technical details, maintenance notes, and routing information.
*   **Airflow Mode:** A visual simulation showing how cold air enters through the intentional empty gaps (U4, U6) and flows upwards through the heat-generating equipment before being exhausted by the top fans. 
*   **Power View Mode:** Highlights the physical power topology. It visually separates critical equipment plugged into the **Green UPS Battery Backup** (maintaining network/storage during an outage) from secondary A/V equipment plugged into the **Orange CyberPower Surge Strip** (safely drops during an outage to save battery).
*   **Complex Routing Diagram:** Clicking on Unit 9 reveals a dynamic flowchart that demystifies the SDI-to-HDMI conversion, splitting, and Ethernet transmission routing for the Sisters' TVs and Projector systems.

---

## 🏗️ Part 2: Physical Rack Layout (15-Unit Breakdown)

The rack is wall-mounted roughly 5.5 feet off the ground. The organization strictly follows principles of **thermodynamics** (heat rises, cool air intakes) and **structural safety** (heaviest items at the bottom).

| Unit | System | Description & Purpose |
| :--- | :--- | :--- |
| **U1** | **UPS Battery Backup** | *Heaviest unit.* Placed at the absolute bottom to reduce structural leverage on the wall-mount bolts. Powers only the NAS and Network Switch. |
| **U2** | **CyberPower PDU** | Main 10-switch power strip. Powers the ATEM, Web Presenter, and AV systems. Placed low to keep thick power cables out of the upper airflow paths. |
| **U3** | **Synology RAID NAS** | Network Attached Storage. Hard drives are highly sensitive to heat. Placed at the bottom to guarantee it intakes the absolute coldest air in the room. |
| **U4** | **EMPTY (Intake)** | Deliberately un-paneled. Acts as a fresh air intake vent for the video processing gear. |
| **U5** | **ATEM & Web Presenter** | Live broadcast hub. Processes SDI camera feeds and encodes the livestream. Runs very warm. |
| **U6** | **EMPTY (Intake)** | Deliberately un-paneled. Acts as a fresh air intake for the dense network switch. |
| **U7** | **24-Port Network Switch** | Core PoE (Power over Ethernet) switch. Handles data routing, IP camera power, and internal network traffic. |
| **U8** | **24-Port Patch Panel** | Terminates all hardwired Cat6 wall-runs from the building. *(See Part 3 for detailed breakdown).* |
| **U9** | **Sisters TV & Projectors** | A shelf holding HDMI splitters, SDI converters, and HDMI-over-Ethernet transmitters. Placed directly next to the patch panel for ultra-short cable runs. |
| **U10** | *(AV Overflow)* | Vertical clearance space required for the equipment sitting on the U9 shelf. |
| **U11** | **Announcement TVs** | *Upcoming System.* Will power the announcement displays via PoE. Currently acting as a thermal blanking panel. |
| **U12** | **Blanking Panel** | Solid metal cover. Maintains negative pressure. |
| **U13** | **Blanking Panel** | Solid metal cover. Maintains negative pressure. |
| **U14** | **Blanking Panel** | Solid metal cover. Maintains negative pressure. |
| **U15** | **Blanking Panel** | Directly beneath the top exhaust fans. Sealing U11-U15 forces the fans to pull air from the U4/U6 intakes rather than sucking hot room air through the top front of the rack. |

---

## 🔌 Part 3: Deep Dive - The 24-Port Patch Panel

Unit 8 houses the 24-Port Cat6 Patch Panel. This is the central nervous system of the building's IT and Media wiring. It allows the committee to patch permanent wall/ceiling runs into the network switch (U7) or the AV system (U9) using short, clean cables. 

### Patch Panel Mapping

**🎥 Broadcast Cameras (Yellow Cables)**
These ports terminate the SDI/IP broadcast cameras from the main hall.
*   **Port 1:** Lecture Camera
*   **Port 2:** Khutbah (Pulpit) Camera
*   **Port 3:** Prayer Camera
*   **Port 4:** Back Camera

**💻 Media Office Terminations (White Cables)**
These ports correspond to the physical Ethernet wall jacks located around the media office for committee workstations.
*   **Ports 8 through 16:** Media Office internal wall plugs.

**📺 A/V & Auxiliary Routing (Basement & Sisters)**
These ports are used primarily by the HDMI-over-Ethernet transmitters located in U9. They carry A/V signals rather than standard network data.
*   **Port 19:** **Basement Feed.** Cat6 cable running directly to the basement area (used for overflow A/V transmission).
*   **Port 20:** **Sisters' Prayer Area (Primary).** Cat6 run to the Sisters' section HDMI receiver.
*   **Port 21:** **Sisters' Prayer Area (Secondary).** Additional Cat6 run to the Sisters' section for backup, additional displays, or future expansion.

**🌐 Network Backbone & Uplinks**
These are critical IT infrastructure ports.
*   **Port 22:** **API / Access Point.** Uplink for the local wireless Access Point, providing Wi-Fi to the area.
*   **Port 23:** **MDF Upstream 1.** Primary fiber/Cat6 trunk line running to the Main Distribution Frame (MDF) where the ISP modem/router lives.
*   **Port 24:** **MDF Upstream 2.** Secondary trunk line running to the MDF. Combined with Port 23, this can act as a Link Aggregation Group (LAG) for double bandwidth (e.g., 20Gbps), or as a failover redundancy to ensure the rack never loses internet.

---

## 🛠️ Part 4: Maintenance Protocols

To ensure the longevity of the equipment in this hot-corner environment, follow these standard operating procedures:

1.  **Dust Mitigation:** The empty units (U4, U6) will naturally accumulate dust as they act as air intakes. Use compressed air to blow out the ATEM, Web Presenter, and Switch vents **at least once every two weeks**.
2.  **Cable Discipline:** Absolutely no cables should drape horizontally across the back of the rack. Power cables route down the right side; Data/AV cables route down the left. 
3.  **Power Outage Protocol:** Do not manually switch off the UPS. Let it safely keep the NAS and Network Switch running. The CyberPower strip will naturally lose power, turning off the ATEM and TVs to conserve building power.
4.  **Blanking Panels:** Under no circumstances should the blanking panels (U12-U15) be removed permanently. Removing them will destroy the "chimney effect" and cause the lower units to overheat.