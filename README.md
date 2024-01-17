This repo contains DeLorean diagnosis and recovery framework code and dataset. 

-`/simulator` contains DeLorean implementation in ArduPilot SITL.
-`/data` contains dataset.

## Running SITL 
Follow the steps given [here](http://ardupilot.org/dev/docs/copter-sitl-mavproxy-tutorial.html) to setup the build environment. 

Clone the project 
```bash
cd simulator/ArduCopter/
../Tools/autotest/sim_vehicle.py --console --map
```

## Launch Missions
/missions contains various types of mission paths.
 
To run mission in the SITL window run the following commands: 
```bash 
wp load ../missions/mission-1.txt
mode guided
arm throttle
takeoff 50
mode auto
```

## Launch Attacks 
The attacks details are in `AP_InertialNav_NavEKF.cpp` and `AP_AHRS_NavEKF.cpp` files. 

Run the following commands to launch sensor attacks. Follows steps shown [here](https://github.com/KimHyungSub/Robotic-vehicle-software-tutorial/tree/main/ArduPilot) to identify the paremeters for each sensor.

GPS Spoofing

```bash 
param set SIM_GPS_GLITCH_X 0.01
param set SIM_GPS_GLITCH_Y 0.01
```

Gyroscope Attack

```bash
param set SIM_GYR1_RND 3
```

## Data Extraction and Pre-Processing 
Convert .bin logs to CSV files as shown below: 

```bash
cd ./data/
python mavlogdump.py --format csv --types ATT <input> <output>
```

`ATT` extracts attitude data. For full list of parameters check [here](https://ardupilot.org/copter/docs/common-downloading-and-analyzing-data-logs-in-mission-planner.html)


## Paper
If you find the repo useful, please cite the following paper:

*Pritam Dash, Guanpeng Li, Mehdi Karimibiuki, and Karthik Pattabiraman, "Diagnosis-guided Attack Recovery for Securing Robotic Vehicles from Sensor Deception Attacks", ACM AsiaCCS 2024.*




