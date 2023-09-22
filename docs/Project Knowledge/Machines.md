# Overview of Machines at CMTI

## Introduction

This section will have information about the different machines available at cmti, such as their information model, method for getting data etc

## Mac Power Mono 200

The machine details are given below:

| S.No | Title            | Information        |
|------|------------------|--------------------|
| 1    | Machine Name     | Mac Power Mono 200 |
| 2.   | Machine Builder  | Mac Power          |
| 3.   | Model            | Mono 200           |
| 4.   | Type             | Turning Center     |
| 5.   | Controller       | Seimens            |
| 6.   | Controller Model | 828D               |

### Information Model

    1. ACTUAL_PART_COUNT_MONO-200
    2. Alarm
        2.1. ALARM
        2.2. ALARM_NUMBER_MONO-200
        2.3. ALARM_TEXTINDEX_MONO-200
        2.4. ALARM_TIME_MONO-200
    3. CNC
        3.1. CNC_MODE_MONO-200
        3.2. CNC_STATE_MONO-200
    4. CUTTING_TIME_MONO-200
    5. Cycle
        5.1. CYCLE_RUNNING_MONO-200
        5.2. CYCLE_START_PB_MONO-200
        5.3. CYCLE_STOP_PB_MONO-200
        5.4. CYCLE_TIME_MONO-200
    6. DISCONNECT
    7. Disconnect_MONO-200
    8. Emergency
        8.1. EMERGENCY
        8.2. EMERGENCY_SIGNAL_MONO-200
    9. MANUAL
    10. NC
        10.1. NC_CHANNEL_RESET_MONO-200
        10.2. NC_RUNNING_MONO-200
        10.3. NC_STOP_MONO-200
    11. OPERATE
    12. OPERATING_TIME_MONO-200
    13. OperatorID
    14. PROG_NAME_MONO-200
    15. Product
        15.1. ProductName
        15.2. ProductResultNumber
        15.3. ProductSerialNumber
    16. Servo
        16.1. Feedrate
            16.1.1. SERVO_AXIS_X_FEEDRATE_MONO-200
            16.1.2. SERVO_AXIS_Z_FEEDRATE_MONO-200
        16.2. Load
            16.2.1. SERVO_DRIVE_LOAD_MONO-200
        16.3. Position
            16.3.1. SERVO_AXIS_X_POSITION_MONO-200
            16.3.2. SERVO_AXIS_Z_POSITION_MONO-200
    17. Spindle
        17.1. Load
            17.1.1. SPINDLE_ACT_LOAD_MONO-200
        17.2. Speed
            17.2.1. SPINDLE_ACT_SPEED_MONO-200
    18. STOP
    19. SUSPEND
    20. TOOL_NO_MONO-200
    21. WARMUP
    22. WARNING

## AMS MCV - 450

The machine details are given below:

| S.No | Title            | Information                    |
|------|------------------|--------------------------------|
| 1.   | Machine Name     | AMS MCV - 450                  |
| 2.   | Machine Builder  | AMS(ACE MANUFACTURING SYSTEMS) |
| 3.   | Model            | MCV - 450                      |
| 4.   | Type             | Milling Center                 |
| 5.   | Controller       | Fanuc                          |
| 6.   | Controller Model | 0i - Mf Plus                   |
| 7.   | Ip Address       | 172.18.30.147                  |

### Information Model

    1. ALARM
    2. Position
    1. Absolute Position
        1. AbsPos_0_path1_MCV-450
        2. AbsPos_1_path1_MCV-450
        3. AbsPos_2_path1_MCV-450
    2. Relative Position
        1. RelPos_0_path1_MCV-450
        2. RelPos_1_path1_MCV-450
        3. RelPos_2_path1_MCV-450
    3. Machine Position
        1. McnPos_0_path1_MCV-450
        2. McnPos_1_path1_MCV-450
        3. McnPos_2_path1_MCV-450
    3. Comment
        1. ActComment_path1_MCV-450
    4. Actual F
        1. ActF_path1_MCV-450
    5. Actual FDec
        1. ActFdec_path1_MCV-450
    6. Actual Program
        1. ActProgram_path1_MCV-450
    7. Actual S
        1. ActS_path1_MCV-450
    8. Battery
        1. APC
            1. Low (APC Battery Low APC could refer to automatic pallet changer - Automatic pallet changers are devices that transfer loads from one pallet to another in a fast and gentle way. They are used to increase productivity, efficiency and flexibility in various industries such as logistics, manufacturing, packaging and machining. Some CNC machines have automatic pallet changers that allow them to switch between different workpieces or parts without interrupting the machining process. This reduces the downtime and increases the output of the CNC machines. Doubt)
                1. ApcBatLow_0_path1_MCV-450
                2. ApcBatLow_1_path1_MCV-450
                3. ApcBatLow_2_path1_MCV-450
            2. Zero
                1. ApcBatZero_0_path1_MCV-450
                2. ApcBatZero_1_path1_MCV-450
                3. ApcBatZero_2_path1_MCV-450
        2. CNC 
            1. Low
                1. CncBatLow_0_path1_MCV-450
                2. CncBatLow_1_path1_MCV-450
                3. CncBatLow_2_path1_MCV-450
        3. Ind Bat Zero (InductoSync Battery Voltage)
            1. IndBatZero_0_path1_MCV-450
            2. IndBatZero_1_path1_MCV-450
            3. IndBatZero_2_path1_MCV-450
        4. S Spd Battery Zero (Serial Separate Detector Battery Voltage)
            1. SSpdBatZero_0_path1_MCV-450
            2. SSpdBatZero_1_path1_MCV-450
            3. SSpdBatZero_2_path1_MCV-450
        5. S Spd Battery Zero (Separate Detector Battery Voltage)
            1. SpdBatZero_0_path1_MCV-450
            2. SpdBatZero_1_path1_MCV-450
            3. SpdBatZero_2_path1_MCV-450
    9. CNC Fan
        1. Speed
            1. CncFan1Speed_path1_MCV-450
            2. CncFan2Speed_path1_MCV-450
            3. CncFan3Speed_path1_MCV-450
            4. CncFan4Speed_path1_MCV-450
        2. Status
            1. CncFan1Status_path1_MCV-450
            2. CncFan2Status_path1_MCV-450
            3. CncFan3Status_path1_MCV-450
            4. CncFan4Status_path1_MCV-450
    10.  CNC State
        1. CncState_path1_MCV-450
    11.  CNC Warning
        1. CncWarning_path1_MCV-450
    12.  Cut Time
        1. CutTime_path1_MCV-450
    13. DISCONNECT
    14. Disconnect_MCV-450
    15. EMERGENCY
    16. EMG_path1_MCV-450
    17.  Inside Fan
        1. Spindle 
            1. Amp (In CNC (Computer Numerical Control) machines, a spindle amplifier is an electronic component that controls the speed and torque of the spindle motor. The spindle motor is a critical component of the machine, and its speed and torque must be carefully controlled during operation to achieve accurate cuts and other machining operations. The spindle amplifier is responsible for receiving signals from the CNC controller and converting them into the appropriate output signals to control the spindle motor. The amplifier typically uses pulse width modulation (PWM) to control the power delivered to the motor, and it may also use feedback from sensors to monitor and adjust the motor's speed and torque. The spindle amplifier may be integrated into the CNC machine's control system, or it may be a separate standalone component. The specific design and capabilities of the spindle amplifier can vary depending on the machine's requirements, but it is typically designed to provide precise control over the spindle motor's speed and torque, as well as protection against overloading and other potential issues. In summary, the spindle amplifier is an important component of CNC machines that plays a critical role in controlling the speed and torque of the spindle motor, which is essential for achieving accurate and precise machining operations. CNC machines often have a fan or other cooling system to help regulate the temperature of the spindle amplifier.)
                1. Speed
                    1. InFan1SpindleAmpSpeed_0_path1_MCV-450
                    2. InFan2SpindleAmpSpeed_0_path1_MCV-450
                2. Status
                    1. InFan1SpindleAmpStatus_0_path1_MCV-450
                    2. InFan2SpindleAmpStatus_0_path1_MCV-450
            2. Com Pw (Common Power) (Spindle motor common power inside cooling fan)
                1. Speed
                    1. InFan1SpdlComPwSpeed_0_path1_MCV-450
                    2. InFan2SpdlComPwSpeed_0_path1_MCV-450
                2. Status
                    1. InFan1SpdlComPwStatus_0_path1_MCV-450
                    2. InFan2SpdlComPwStatus_0_path1_MCV-450
        2. Servo 
            1. Amp 
                1. Speed
                    1. Fan 1
                    1. InFan1SrvAmpSpeed_0_path1_MCV-450
                    2. InFan1SrvAmpSpeed_1_path1_MCV-450
                    3. InFan1SrvAmpSpeed_2_path1_MCV-450
                    2. Fan 2
                    1. InFan2SrvAmpSpeed_0_path1_MCV-450
                    2. InFan2SrvAmpSpeed_1_path1_MCV-450
                    3. InFan2SrvAmpSpeed_2_path1_MCV-450
                2. Status
                    1. Fan 1
                    1. InFan1SrvAmpStatus_0_path1_MCV-450
                    2. InFan1SrvAmpStatus_1_path1_MCV-450
                    3. InFan1SrvAmpStatus_2_path1_MCV-450
                    2. Fan 2
                    1. InFan2SrvAmpStatus_0_path1_MCV-450
                    2. InFan2SrvAmpStatus_1_path1_MCV-450
                    3. InFan2SrvAmpStatus_2_path1_MCV-450
            2. Com Pw (Common Power) (Spindle motor common power inside cooling fan)
                1. Speed
                    1. Fan 1
                    1. InFan1SrvComPwSpeed_0_path1_MCV-450
                    2. InFan1SrvComPwSpeed_1_path1_MCV-450
                    3. InFan1SrvComPwSpeed_2_path1_MCV-450
                    2. Fan 2
                    1. InFan2SrvComPwSpeed_0_path1_MCV-450
                    2. InFan2SrvComPwSpeed_1_path1_MCV-450
                    3. InFan2SrvComPwSpeed_2_path1_MCV-450
                2. Status
                    1. Fan 1
                    1. InFan1SrvComPwStatus_0_path1_MCV-450
                    2. InFan1SrvComPwStatus_1_path1_MCV-450
                    3. InFan1SrvComPwStatus_2_path1_MCV-450
                    2. Fan 2
                    1. InFan2SrvComPwStatus_0_path1_MCV-450
                    2. InFan2SrvComPwStatus_1_path1_MCV-450
                    3. InFan2SrvComPwStatus_2_path1_MCV-450
    18. MANUAL
    19. Macro Variable
        1. MacroVar_575_path1_MCV-450
        2. MacroVar_576_path1_MCV-450
    20. Main Comment
        1. MainComment_path1_MCV-450
    21. Main Program
        1. MainProgram_path1_MCV-450
    22. Modal
        1. ModalF_path1_MCV-450
        2. ModalM2_path1_MCV-450
        3. ModalM3_path1_MCV-450
        4. ModalM_path1_MCV-450
        5. ModalS_path1_MCV-450
        6. ModalT_path1_MCV-450
    23. Mode
        1. Mode_path1_MCV-450
    24. OPERATE
    25. OperatorID
    26. Override
        1. Override_path1_MCV-450
    27. Total Number of parts Made
        1. PartsNumAll_path1_MCV-450
    28. Parts made in this session (after the machine was turned on currently). Doubt
        1. PartsNum_path1_MCV-450
    29. Power On time
        1. PowOnTime_path1_MCV-450
    30. Product Data
        1. Product Name
            1. ProductName
        2. Product Result Number
            1. ProductResultNumber
        3. Product Serial Number
            1. ProductSerialNumber
    31. Encoder Temperature
        1. PulseCoderTemp_0_path1_MCV-450
        2. PulseCoderTemp_1_path1_MCV-450
        3. PulseCoderTemp_2_path1_MCV-450
    32. Radiator Fan
        1. Spdl 
            1. Amplifier
                1. Speed
                    1. RadFan1SpindleAmpSpeed_0_path1_MCV-450
                    2. RadFan2SpindleAmpSpeed_0_path1_MCV-450
                2. Status
                    1. RadFan1SpindleAmpStatus_0_path1_MCV-450
                    2. RadFan2SpindleAmpStatus_0_path1_MCV-450
            2. Com Pw 
                1. Speed
                    1. RadFan1SpdlComPwSpeed_0_path1_MCV-450
                    2. RadFan2SpdlComPwSpeed_0_path1_MCV-450
                2. Status
                    1. RadFan1SpdlComPwStatus_0_path1_MCV-450
                    2. RadFan2SpdlComPwStatus_0_path1_MCV-450
        2. Servo 
            1. Amplifier 
                1. Speed
                    1. Fan 1
                    1. RadFan1SrvAmpSpeed_0_path1_MCV-450
                    2. RadFan1SrvAmpSpeed_1_path1_MCV-450
                    3. RadFan1SrvAmpSpeed_2_path1_MCV-450
                    2. Fan 2
                    1. RadFan2SrvAmpSpeed_0_path1_MCV-450
                    2. RadFan2SrvAmpSpeed_1_path1_MCV-450
                    3. RadFan2SrvAmpSpeed_2_path1_MCV-450
                2. Status
                    1. Fan 1
                    1. RadFan1SrvAmpStatus_0_path1_MCV-450
                    2. RadFan1SrvAmpStatus_1_path1_MCV-450
                    3. RadFan1SrvAmpStatus_2_path1_MCV-450
                    2. Fan 2
                    1. RadFan2SrvAmpStatus_0_path1_MCV-450
                    2. RadFan2SrvAmpStatus_1_path1_MCV-450
                    3. RadFan2SrvAmpStatus_2_path1_MCV-450
            2. Com Pw 
                1. Speed
                    1. Fan 1
                    1. RadFan1SrvComPwSpeed_0_path1_MCV-450
                    2. RadFan1SrvComPwSpeed_1_path1_MCV-450
                    3. RadFan1SrvComPwSpeed_2_path1_MCV-450
                    2. Fan 2
                    1. RadFan2SrvComPwSpeed_0_path1_MCV-450
                    2. RadFan2SrvComPwSpeed_1_path1_MCV-450
                    3. RadFan2SrvComPwSpeed_2_path1_MCV-450
                2. Status
                    1. Fan 1
                    1. RadFan1SrvComPwStatus_0_path1_MCV-450
                    2. RadFan1SrvComPwStatus_1_path1_MCV-450
                    3. RadFan1SrvComPwStatus_2_path1_MCV-450
                    2. Fan 2
                    1. RadFan2SrvComPwStatus_0_path1_MCV-450
                    2. RadFan2SrvComPwStatus_1_path1_MCV-450
                    3. RadFan2SrvComPwStatus_2_path1_MCV-450
    33. Run Time
        1. RunTime_path1_MCV-450
    34. STOP
    35. SUSPEND
    36. Sequence
        1. Sequence_path1_MCV-450
    37. Servo
        1. Current
            1. Percentage (Servo Current Percentage parameter might be related to the servo current percentage of the Fanuc controller. Servo current is the amount of electric current that flows through the servo motor, which controls the movement of the machine axes. The parameter value might indicate how much of the maximum servo current is being used by the controller.)
                1. ServoCurrentPer_0_path1_MCV-450
                2. ServoCurrentPer_1_path1_MCV-450
                3. ServoCurrentPer_2_path1_MCV-450
            2. Value (Servo Current )
                1. ServoCurrent_0_path1_MCV-450
                2. ServoCurrent_1_path1_MCV-450
                3. ServoCurrent_2_path1_MCV-450
        2. Error
            1. ServoError_0_path1_MCV-450
            2. ServoError_1_path1_MCV-450
            3. ServoError_2_path1_MCV-450
    38. Servo 
        1. Leak Resistance (Servo leak resistance is a measure of how much the servo motor resists unwanted movement or vibration when it is not powered. Maybe this parameter is used to calibrate or monitor the servo leak resistance of your machine. It could also be servo insulation resistance which is a measure of how well the servo motor is insulated from electric currents that could damage it or cause interference. Maybe this parameter is used to check or adjust the servo insulation resistance of your machine.)
            1. ServoLeakResistData_0_path1_MCV-450
            2. ServoLeakResistData_1_path1_MCV-450
            3. ServoLeakResistData_2_path1_MCV-450
        2. Load
            1. ServoLoad_0_path1_MCV-450
            2. ServoLoad_1_path1_MCV-450
            3. ServoLoad_2_path1_MCV-450
        3. Speed
            1. ServoSpeed_0_path1_MCV-450
            2. ServoSpeed_1_path1_MCV-450
            3. ServoSpeed_2_path1_MCV-450
        4. Temperature
            1. ServoTemp_0_path1_MCV-450
            2. ServoTemp_1_path1_MCV-450
            3. ServoTemp_2_path1_MCV-450
    39. Signal Related Parameters (unknown)
        1. SigAL_path1_MCV-450
        2. SigCUT_path1_MCV-450
        3. SigDM00_path1_MCV-450
        4. SigDM01_path1_MCV-450
        5. SigENB_0_path1_MCV-450
        6. SigINP_0_path1_MCV-450
        7. SigINP_1_path1_MCV-450
        8. SigINP_2_path1_MCV-450
        9. SigMDRN_path1_MCV-450
        10. SigOP_path1_MCV-450
        11. SigSBK_path1_MCV-450
        12. SigSPL_path1_MCV-450
        13. SigSTL_path1_MCV-450
    40. Spindle
        1. Leak Resistance
            1. SpindleLeakResistData_0_path1_MCV-450
        2. Load
            1. SpindleLoad_0_path1_MCV-450
        3. Speed
            1. SpindleSpeed_0_path1_MCV-450
        4. Temperature
            1. SpindleTemp_0_path1_MCV-450
        5. Total Revolution
            1. SpindleTotalRev1_0_path1_MCV-450
            2. SpindleTotalRev2_0_path1_MCV-450
    41. WARMUP
    42. WARNING


## Mazak Mazatech H-400N

The machine details are given below:

| S.No | Title                               | Information                                  |
|------|-------------------------------------|----------------------------------------------|
| 1.   | Machine Name                        | Mazak Mazatech H-400N                        |
| 2.   | Machine Builder                     | Machine Builder                              |
| 3.   | Model                               | H-400 N (Mazatech line of machining centers) |
| 4.   | Type                                | Milling Machine                              |
| 5.   | Controller                          | Fanuc                                        |
| 6.   | Controller Type                     | 0i -md series                                |
| 7.   | Ip Address                          | 172.18.30.157                                |
| 8.   | Mac Address                         | 00E0E41B3630                                 |
| 9.   | Application Layer for Communication | Focas                                        |


### Overview of Mazak
Mazak is a prominent global manufacturer of machine tools, with a rich history dating back to its establishment in Japan in 1919. Over the years, the company has expanded its operations worldwide and has become a renowned name in the industry.

### Mazatech: Precision and Versatility in Machining Centers
*Mazatech* is a specialized product line within Mazak that focuses on the development and production of machining centers. These machines are highly regarded for their precision, versatility, and advanced features, making them suitable for a wide range of machining applications.

### Introducing the H-400N Machining Center
The **H-400N** is a specific model within the Mazatech line of machining centers. While detailed specifications about this particular model are not available due to the training data limitations up until September 2021, it is inferred that the H-400N is designed to handle medium to large-scale machining operations. It is likely optimized for high-speed and high-precision applications.

### Fanuc: Leading the Industry in CNC Systems
*Fanuc* is a well-known Japanese company specializing in the manufacturing of industrial robots, CNC systems, and factory automation solutions. They are a major supplier of CNC systems to various machine tool manufacturers, including Mazak.

### Exploring the Fanuc 0i -md Series
The **0i -md** series refers to a specific family or generation of Fanuc CNC systems. The "0i" represents the overall series or platform, while the "-md" indicates its specific focus on milling and drilling applications. Fanuc 0i CNC systems are renowned for their reliability, user-friendly interface, and advanced capabilities, providing precise control over the machining process.

### Note on Variations and Updates
It is important to note that the specific capabilities, features, and technical specifications of the Mazak H-400N and the Fanuc 0i -md series may vary, as machine models and CNC systems often offer different configurations and options. For the most accurate and up-to-date information, it is recommended to consult the official Mazak and Fanuc websites or reach out to their representatives directly.