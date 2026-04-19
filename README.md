**Farm Disaster Hub** 🌱  
**Predict. Alert. Protect.** *Track 2: GW Global Food Institute \- Problem Statement 3* (*Feeding Communities When It Matters Most*)

Farm Disaster Hub (FDH) is an open-source, IoT-enabled early warning system designed to strengthen food access for vulnerable agricultural communities before, during, and after natural disasters. By utilizing a localized web of predictive environmental sensors, FDH does not just warn a farmer of an impending disaster that could destroy crop yields–it acts as an automated, rapid-response marketplace that instantly pings local food banks, relief workers, and community organizations to secure harvests before they are destroyed.

Targeting fragile supply chains of local farmers and the Global South, this solar-powered, off-grid solution aligns directly with the United Nations Sustainable Development Goals:

- **SDG 2 (Zero Hunger):** Protecting food supply at the origin and securing emergency access to harvests  
- **SDG 13 (Climate Action):** Strengthening community resilience to climate-related hazards  
- **SDG 17 (Partnerships for the Goals):** Forging real-time, automated collaborations between private agriculture and humanitarian organizations

**System Architecture 🛠**  
FDH operates through a seamless integration of off-grid hardware, continuous machine learning, and a frictionless mobile alert ecosystem.

1. **The Edge Hardware Node**  
   Our 24-hour prototype utilizes an affordable, easily scalable hardware stack:  
* **Compute:** Raspberry Pi  
* **Power:** MakerFocus Raspberry Pi 4 Battery Pack UPS (V3Plus Expansion Board with 10000mAh Battery) paired with a solar charging module. This ensures the 18650 battery cells keep the system fully operational during dark, storm-heavy conditions  
* **Sensors:** Ambient Temperature Sensor & Grove Air Quality Sensor v1.3.

  *(Note: Our hackathon prototype utilizes a generalized TVOC sensor using a mathematical heuristic to estimate PPMs. Production nodes are designed to house three dedicated sensors for precise Carbon Monoxide, Formaldehyde, and Acetone isolation).*

* **Enclosure:** Modeled for extreme weather survivability, the CAD housing applies aerodynamic principles to withstand severe wind shear during hurricane events. Structural transitions and chamfers on the external mounts are precisely drafted to yield circular, structurally sound bases to prevent localized stress fracturing during seismic or high-impact events.

2. **The Predictive AI Model**  
   The core detection engine is a TensorFlow.js multi-class neural network trained to detect the localized chemical “fingerprints” of specific disasters using the following output labels:  
* **0 \- Normal Air:** Standard baseline metrics  
* **1 \- Wildfire:** Massive Carbon Monoxide (CO) and temperature spikes derived from EPA historical maximums.  
* **2 \- Flooding / Crop Rot:** Anaerobic decomposition releasing high levels of Acetone/Ethanol alongside plummeting temperatures (based on NIH biochemistry data and NOAA meteorological models).  
* **3 \- Earthquake / Chemical Spill:** Instantaneous, violent spikes in Formaldehyde/Benzene representing structural failures and ruptured agricultural tanks (exceeding OSHA STEL limits).  
    
3. **Human-in-the-Loop (HITL) Continuous Learning**  
   The mobile application features a highly accessible, universally recognizable icon-based UI. When an anomaly is detected, farmers receive a push notification allowing them to hit “**CONFIRM”** or **“FALSE ALARM.”**  
   This triggers a continuous learning pipeline. The Node.js backend captures that exact moment of raw sensor data, pairs it with the farmer’s confirmed label, and compiles it in the central database. This crowdsourced data periodically recompiles the model, making the algorithm smarter and hyper-tailored to the region’s micro-climate every day.

**Installation & Setup 🚀** 

**Prerequisites**

* Raspberry Pi (3B+/4B/5/Zero W) running Raspberry Pi OS  
* Node.js (v16.x or higher)  
* npm (Node Package Manager)

1. **Clone the Repository**

git clone https://github.com/farmequipped/farmdisasterhub

2. **Install Dependencies**

npm install express  
npm install path  
npm install http  
npm install nodemailer  
npm install bonjour  
npm install fs  
npm install dotenv  
npm install child\_process  
pip install time  
pip install numpy  
pip install request  
pip install tensorflow  
pip install board  
pip install adafruit\_dht  
pip install busio  
pip install digitalio

*This installs the required packages, including* express, socket.io, tensorflow, and the necessary sensor libraries

3. **Hardware Wiring**

* Connect the **Temperature Sensor** to the assigned GPIO data pin  
* Connect the **Grove Air Quality Sensor** to the analog input (using an ADC converter if required for your specific Pi model).  
* *Ensure the UPS HAT is properly mounted to safely manage power draw between the solar array and the Pi*

4. **Run the Local Server**

node server.js

The Node.js server will initialize, host the local web dashboard, and establish the Socket.io connections. The terminal will log the active port (default is http://localhost:3000).

**User Interfaces 📱**  

**The Farmer Node:** A mobile view optimized for high contrast, utilizing Socket.io push notifications to alert the farmer and display the HITL report/confirmation buttons  
**The Relief Worker Dashboard:** Accessed via the web server, this UI acts as a regional intelligence network map, displaying active disaster alerts and the locations of emergency harvests available for immediate local distribution

**Dataset & Training Information 📊**   

Due to the niche hardware parameters, the initial model weights were trained using a heuristically derived synthetic dataset grounded in strict federal and scientific baselines:

* **EPA Outdoor Air Quality Data:** California 2020 (ad\_viz\_plotval\_data.csv)  
* **OpenFEMA Dataset:** Disaster Declarations Summaries v2  
* **OSHA:** Formaldehyde standard 1910.1048  
* **NIH:** Anaerobic decomposition and fermentation baseline records

**License 📄** 

* This project is licensed under the **MIT License**. We believe that early warning systems for vulnerable populations should be open, accessible, and scalable without proprietary barriers.