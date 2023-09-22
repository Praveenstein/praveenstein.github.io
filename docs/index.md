# Introduction

This project is implemented to help the maintenace team of Toyota Industries Engine India Private Limited (here by called as TIEI) to help in machine maintenace activities of their new plant.

## Requirements of the Project

The project requirements are:

- **Machine Maintenace** - Machines (General purpose machines such as cnc and special purpose machines such as laser cladding) need to monitored for any abnormal conditions.

- **Real Time Data Visualization Feature** - A graphical way to visualize the data from all these machines.

- **Spare Part Management** - A system to monitor part count of machines and alerts system to notify maintenace team when a part of a machine needs to be replaced (which is monitored from a critical limit for the part).

- **Alarm Management** - A system to generate a summary of alarms for machines.

- **Email Alerts & Report Generation** - A system to send email alerts when a machine is in abnormal state and to generate summart report of machines under abnormal states.

- **Separate Database for the Machine Data** - A new database where a copy data from the existing mongodb database will exist, and all processing and analytics should be implemeted with that data.

## Nature of the Current System at TIEI

The Exisitng machines at CMTI's SMDDC are:

### Machine

The following table gives the summary of available machines at TIEI:

| S.No 	| Machine Name           	| Type           	| Description                                                              	| Brand                          	| Model            	| Location 	| Controller Name 	| Controller Model 	| Legacy 	| Ip Address  	|
|------	|------------------------	|----------------	|--------------------------------------------------------------------------	|--------------------------------	|------------------	|----------	|-----------------	|------------------	|--------	|-------------	|
| 1.   	| Ace LT-2               	| Turning Center 	| 2-axes horizontal turning centres                                        	| Ace Micromatic                 	| LT-2-LM-500-PLUS 	| R1       	| Fanuc           	| 0i tf plus       	| No     	| 172.18.7.27 	|
| 2.   	| MONO 200               	| Turning Center 	| MONO-200 is a CNC turning center machine                                 	| Mac Power                      	| Mono 200         	| R2       	| Seimens         	| sinumerik 828d   	| No     	| 172.18.7.27 	|
| 3.   	| AMS MCV - 450          	| Milling Center 	| It's vertical machining center, It has a Fanuc 0i-MF plus CNC controller 	| AMS(ACE MANUFACTURING SYSTEMS) 	| MCV - 450        	| R3       	| Fanuc           	| 0i - Mf Plus     	| No     	| 172.18.7.27 	|
| 4.   	| Mazak - H-400 N        	| Milling Center 	| Mazak H-400N is a horizontal machining center with a Seimens Controller  	| Mazak                          	| H-400N           	| R4       	| Seimens         	| sinumerik 828D   	| No     	| 172.18.7.27 	|
| 5.   	| Mazak - H-400 N        	| Milling Center 	| Mazak H-400N is a horizontal machining center with a Fanuc Controller    	| Mazak                          	| H-400N           	| L4       	| Fanuc           	| 0i -md           	| TBA    	|             	|
| 6.   	| Hmt - vtc 800, seimens 	| Milling Center 	|                                                                          	| HMT                            	| VTC - 800        	| L3       	| Seimens         	| TBA              	| Yes    	|             	|
| 7.   	| Schaublin 33 cnc       	| Milling Center 	|                                                                          	| Schaublin Machines SA          	| 33 CNC           	| L2       	| Seimens         	| 840D             	| Yes    	|             	|
| 8.   	| Hmt Stallion 200       	| Turning Center 	|                                                                          	| HMT                            	| Stallion         	| L1       	| Fanuc           	| ot - Series      	| Yes    	|             	|

### Machine Parameters

The machine parameters (for the 59 general purpose cnc machines) are split into 17 groups of two types:

- **Static Parameters** - These are the parameters that have a single value as their critical limits, for example, the warning limit of encoder temperature could be 50 degree celcius and critical limit could be 60 degree celcius. Hence if any of the static parameter, goes beyond these limits, it is said to be in abnormal state.

- **Dynamic Parameters** - These are the parameters have a set of values (also know as reference signals). If any new set of values (for a new machining cycle) is not similar to the reference signal, it will be considered to be in abnormal state.

The group of parameters are shown in the table below.


| S.No 	| Parameter Group                                                 	| Type    	|
|------	|-----------------------------------------------------------------	|---------	|
| 1.   	| APC Battery                                                     	| Static  	|
| 2.   	| CNC Battery                                                     	| Static  	|
| 3.   	| Servo and Spindle Motor Temperature                             	| Static  	|
| 4.   	| Encoder Temperature                                             	| Static  	|
| 5.   	| Spindle and Servo Motor Insulation Resistance                   	| Static  	|
| 6.   	| CNC Fan Speeds                                                  	| Static  	|
| 7.   	| Internal Fan 1 Power Supply - Spindle Motor & Spindle Amplifier 	| Static  	|
| 8.   	| Internal Fan 1 Servo Amplifier                                  	| Static  	|
| 9.   	| Internal Fan 1 Power Supply - Servo Motor                       	| Static  	|
| 10.  	| Internal Fan 2 Power Supply - Spindle Motor & Spindle Amplifier 	| Static  	|
| 11.  	| Internal Fan 2 Servo Amplifier                                  	| Static  	|
| 12.  	| Internal Fan 2 Power Supply - Servo Motor                       	| Static  	|
| 13.  	| Battery Zero Separate Detector                                  	| Static  	|
| 14.  	| Battery Zero Serial Separate Detector                           	| Static  	|
| 15.  	| Radiator Fan 1 - Servo & Spindle Amplifier                      	| Static  	|
| 16.  	| Radiator Fan 2 - Servo & Spindle Amplifier                      	| Static  	|
| 17.  	| Servo & Spindle Motor Load                                      	| Dynamic 	|


## Features of the Project

The final solution given to tiei will be a web application with the following features:

- **Maintenace Feature** - This page of the web application will have a summary of states of all machines in visual way.
- **Real Time Data Visualization Feature** - This page of the web application will display time series data for a given machine, for a given parameter group, for a given axis within a given time range.

- **Alarm Management Feature** This page of the web application will display the summary of alarms and events for a given machine, during a given period of time range.

- **Spare Part Management Feature** This section of the web application will have information about the part count of machines, and information about the parts that needs to be replaced when a critical part limit is reached.

- **Special Purpose Machines Feature** This section of the web application will real time visualization of its parameters over a given range of time.

Apart from the web application, the final project solution should include the following services:

- **4/8 Hour Summary Report Generation Service** - A Service which generates a summary of machines that were under abnormal states for every 4/8 hour.
- **Email Alerts Service** - A Service which sends email alerts as soon as a machines goes to abnormal state.