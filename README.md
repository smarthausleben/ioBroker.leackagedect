![Logo](admin/wamo.png)
# ioBroker.wamo

[![NPM version](https://img.shields.io/npm/v/iobroker.wamo.svg)](https://www.npmjs.com/package/iobroker.wamo)
[![Downloads](https://img.shields.io/npm/dm/iobroker.wamo.svg)](https://www.npmjs.com/package/iobroker.wamo)
![Number of Installations](https://iobroker.live/badges/wamo-installed.svg)
![Current version in stable repository](https://iobroker.live/badges/wamo-stable.svg)
[![Dependency Status](https://img.shields.io/david/smarthausleben/iobroker.wamo.svg)](https://david-dm.org/smarthausleben/iobroker.wamo)

[![NPM](https://nodei.co/npm/iobroker.wamo.png?downloads=true)](https://nodei.co/npm/iobroker.wamo/)

**Tests:** ![Test and Release](https://github.com/smarthausleben/ioBroker.wamo/workflows/Test%20and%20Release/badge.svg)

# WAMO adapter for ioBroker

This adapter adds "wamo" leakage protection monitoring to your ioBroker installation.

The adapter connects to your **SYR SafeTech Connect 2422** or **POLYGONVATRO** leakage protection device in order to read data from the device and create some statistic data like water consumption history.

Details about the SYR SaveTech Connect 2422 can be found [here.](https://www.syr.de/de/Produkte/CB9D9A72-BC51-40CE-840E-73401981A519/SafeTech-Connect)

The POLYGONVATRO unit is, under the hood, a SYR SaveTech Connect 2422 unit but without pressure-, temperature- and conductivity sensor. The POLYGONVATRO unit is currently not available. 

## IMPORTENT
Since the **_Jam Protection release_** a scheduled move of the main valve was added and can be activated and scheduled in the adapter settings area (Tab: Tasks)

Be verry careful with this functionality because it will **_close_** and **_open_** the main valve in order to prevent it to get stuck in open position and therefore will not close in case of an leakage.

The **_Jam Protection_** can be planed using a CRON schedule which will also be configured in the adapter settings **_Tasks_** tab.
Be verry careful there as well, because if you schedule a jam protection for example every 1 Minute you are having big trouble because your main valve will close and open every minute!

During the **_Jam Protection_** activity, no regular states (Valve, Alarms etc.) will be updated in order to prevent false trigger you may have set on of those states.

If the main valve is already in **_closed_** position, the **_Jam Protection_** activity will not be performed in order to prevent opening the main valve.
If there is water consumption at start of **_Jam Protection_** the action will be delayed for 1 minute. After 10 faild attempts (water still flowing)  **_Jam Protection_** will be aborted.

### Disclaimer / Warning
If during the **_Jam Protection_** activity communication to the device gets lost or the WAMO adapter or ioBroker itself crashes or will be stopped, the main valve will stay in the last commanded position! This means if something gets wrong, the valve could be closed and needs to be opened by yourself using the related app or the button on the device itself.

## Support this project
If you find this adapter useful and you want to support this project, your kindness will be highly appreciated. You can easily support me [here.](https://www.paypal.com/paypalme/smarthausleben) Thanks 😊   

## Changelog
<!--
    Placeholder for the next version (at the beginning of the line):
    ### **WORK IN PROGRESS**
-->

### **WORK IN PROGRESS**
* (smarthausleben) ADD: [SafeFloor Device] New **SafeFloor Units** Tab in adapter settings to manage up to 4 **_SafeFloor Connect_** devices
* (smarthausleben) ADD: New option **_"Enable executing test loop"_** in Tab **_"Advanced Options"_** to enable/disable cron based executed [Test Loop]
* (smarthausleben) ADD: New option **_"Allow SERVICE and FACTORY state changes"_** in Tab **_"Advanced Options"_** to enable/disable changes of objects protected by the manufacturer 
* (smarthausleben) ADD: State `BFT` - Button filter threshold
* (smarthausleben) ADD: State `BPT` - Button proximity threshold
* (smarthausleben) ADD: State `CNF` - Conductivity factor
* (smarthausleben) ADD: State `CNL` - Conductivity limit
* (smarthausleben) ADD: State `DBD` - MLT pressure drop
* (smarthausleben) ADD: State `DBT` - MLT pressure drop time
* (smarthausleben) ADD: State `DCM` - MLT test time close
* (smarthausleben) ADD: State `DOM` - MLT test time open
* (smarthausleben) ADD: State `DPL` - MLT pulses
* (smarthausleben) ADD: State `DST` - MLT test time NOPULS
* (smarthausleben) ADD: State `DTC` - MLT verification cycles
* (smarthausleben) ADD: State `DTT` - Micro-Leakage-Test start time
* (smarthausleben) ADD: State `HTD` - Disable HTTPS connection (only MQTT)
* (smarthausleben) ADD: State `MQT` - MQTT connection type
* (smarthausleben) ADD: State `MRT` - Maintenance (Husty) server connection
* (smarthausleben) ADD: State `MSC` - MQTT reconnect time
* (smarthausleben) ADD: State `DSV` - Micro-Leakage-Test state
* (smarthausleben) ADD: State `FSL` - Paired Floorsensors list
* (smarthausleben) ADD: State `ALH` - Alarm history file
* (smarthausleben) ADD: State `STH` - Statistics history file
* (smarthausleben) ADD: State `PAH` - Parameters history file
* (smarthausleben) ADD: State `WFL` - WiFi scan
* (smarthausleben) ADD: State `BUZ` - Buzzer parameters
* (smarthausleben) ADD: State `ALM` - Alarm memory
* (smarthausleben) ADD: State `TTM` - Turbine no pulse max. time
* (smarthausleben) ADD: State `TYP` - Safe-Tec type
* (smarthausleben) ADD: State `WNS` - WiFi AP disabled
* (smarthausleben) ADD: State `HWV` - Hardware version
* (smarthausleben) ADD: State `DKI` - Safe-Tec device kind ID
* (smarthausleben) CHG: State `ALD` - Alarm duration (signaling time) can now be changed by user
* (smarthausleben) CHG: State `CLP` - Cluster Profile can now be changed by user
* (smarthausleben) CHG: State `SLO` - Self learning offset can now be changed by user
* (smarthausleben) CHG: State `SLP` - Self learning phase can now be changed by user
* (smarthausleben) CHG: State `SMF` - Self learning minimum flow can now be changed by user
* (smarthausleben) CHG: State `SOF` - Self learning offset flow can now be changed by user

### 0.3.0 (2023-04-04) - ***Jam Protection*** release
* (smarthausleben) ADD: [Main valve jam protection] New State JPR for Jam protection running 
* (smarthausleben) ADD: [Main valve jam protection] New State JPA for Jam protection aktivated
* (smarthausleben) ADD: [Main valve jam protection] New State JPT for Jam protection timing (CRON)
* (smarthausleben) ADD: [Main valve jam protection] New **Task Tab** in adapter settings to manage a scheduled regular movement of the main valve in order to prevent a stuck valve
* (smarthausleben) FIX: [interfaceBusy] flag was not reset after AXIOS interface handler error **_(Issue #21)_**
* (smarthausleben) ADD: [WatchDog] function for interfaceBusy flag. Flag will be reset after defined amount of requests **_(Issue #21)_**

### 0.2.13 (2022-10-12)
* (smarthausleben) add: new property "createOnStartup" in DeviceParameter
* (smarthausleben) add: new property "saveRawData" in DeviceParameter
* (smarthausleben) change: creating all state objects during startup to avoid calling "setObjectNotExistsAsync" later on
* (smarthausleben) add: Profile parameter raw states
* (smarthausleben) change: default value for "factor_german_water_hardnes" changed to 0.0296041666666667
* (smarthausleben) FIX update german water hardnes factor object (GHARDFACTOR) during startup 

### 0.2.12 (2022-09-20)
* (smarthausleben) Release 0.2.12

### 0.2.11 (2022-09-19)
* (smarthausleben) Release 0.2.11

### 0.2.10 (2022-09-19)
* (smarthausleben) state types changed UNI, PSD, CSD, TSD, T2
* (smarthausleben) states changable UNI, PSD, CSD, TSD, T2
* (smarthausleben) added DeviceControls RST (restart device)
* (smarthausleben) new channel DeviceControl
* (smarthausleben) added unit for GHARDNESS (°dH)
* (smarthausleben) new state GHARDFACTOR (calculation factor German water hardnes)

## License
The MIT License (MIT)

Copyright (c) 2022-2023 smarthausleben <info@smarthausleben.de>