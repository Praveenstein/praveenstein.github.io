# Back End

## Introduction

The requirements for the back end are:

1. anyio==3.5.0

1. asgiref==3.5.1

1. bcrypt==3.2.2

1. cffi==1.15.1

1. click==8.1.3

1. colorama==0.4.4

1. cryptography==37.0.4

1. databases==0.5.5

1. ecdsa==0.18.0

1. et-xmlfile==1.1.0

1. fastapi==0.75.2

1. greenlet==1.1.2

1. h11==0.13.0

1. idna==3.3

1. motor==3.0.0

1. numpy==1.22.4

1. openpyxl==3.0.10

1. pandas==1.4.2

1. passlib==1.7.4

1. pony==0.7.16

1. psycopg2==2.9.3

1. pyasn1==0.4.8

1. pycparser==2.21

1. pydantic==1.9.0

1. pymongo==4.1.1

1. python-dateutil==2.8.2

1. python-dotenv==0.20.0

1. python-jose==3.3.0

1. python-multipart==0.0.5

1. pytz==2022.1

1. rsa==4.9

1. six==1.16.0

1. sniffio==1.2.0

1. SQLAlchemy==1.4.35

1. sqlalchemy2-stubs==0.0.2a22

1. sqlmodel==0.0.6

1. starlette==0.17.1

1. typing_extensions==4.2.0

1. uvicorn==0.17.6

1. XlsxWriter~=3.0.3

1. schedule~=1.1.0


## Project layout

    main.py                         # The main entry point for the fastapi backend
                                    # application.
    machine_monitoring_app/
        database/                   # This python package consist of modules related
                                    # to database.
            __init__.py             # The Initialization file for the python package.
            crud_operations.py      # This python module consist of functions to help
                                    # in database CRUD operations.
            db_utils.py             # This python module consist of utility functions
                                    # to help in timescaledb operations.
            mongo_db_utils.py       # This python module consist of utility functions
                                    # to help in mongodb operations.
            mongodb_client.py       # This python module consist of functions to help
                                    # connect with mongodb.
            pony_models.py          # This python module consist of classes for the
                                    # ORMs with timescaledb.
        exception_handling/         # This python package consist of modules related
                                    # to exception handling.
            __init__.py             # The Initialization file for the python package.
            custom_exception.py     # This python module consist of classes for custom
                                    # exception handling.
        models/                     # This python package consist of modules for the
                                    # pydantic classes.
            __init__.py             # The Initialization file for the python package.
            base_data_models.py     # The file consist of base pydantic models.
            request_models.py       # The file consist of pydantic models that are used
                                    # for request body.
            response_models.py      # The file consist of pydantic models that are used
                                    # for response body.
        router/                     # The package consist of all endpoint of this backend.
            __init__.py             # The Initialization file for the python package.
            core_data_route.py      # The consist of core end points for this back end.
            router_dependencies.py  # The file consist of functions to help other end points
                                    # Such as user authentication using jwt tokens.
            security_routes.py      # The file consist of endpoint for user creation
                                    # and login methods.
        utils/                      # The package consist of utility modules
            __init__.py             # The Initialization file for the python package.
            configuration_helper.py # The consist of functions to help in configuration
                                    # Such as logger configuration, database configuration, and 
                                    # Initial server configuration.
            global_variables.py     # The file consist of function to return some common
                                    # Global variables.
        __init__.py                 # The Initialization file for the python package.

## API Endpoints

The back end exposes api's to carry out different functionalites of the web application. The end points are classified into two type, core data routes and security routes. They are explained below.

### Core Data Route

These set of end points consist of all the core routes requrired for data access and manipulation.

#### Get End Points
These are end points used to access data.

1. **/api/v1/machine-state/{parameterGroupId}** - This end point is used to get the status of machines in the given parameter group (such as encoder temperature).
    - **Input Parameter**
        - **parameterGroupId** - This is the id column from the table ParameterGroup to identify the parameter group this parameter belongs to (For example id 4 for group encoder temperature).

    - **Response Body** - The response body will consist of dictionary of two important key values, the first one denotes the status of machines (that are in abnormal condition) and second one is the summary of status of all other parameter groups (17 groups)

    ```json

        {
            "param": 4,
            "param_actual_name": "ENCODER_TEMPERATURE",
            "machines": [
                {
                "name": "T_B_OP160",
                "status": 2,
                "axes": [
                    {
                    "name": 1,
                    "actual_name": "PulseCoderTemp_1_path1_T_B_OP160",
                    "last_update_time": 1662514103,
                    "value": 55,
                    "status": 2
                    }
                ]
                },
                {
                "name": "T_B_OP195A",
                "status": 2,
                "axes": [
                    {
                    "name": 1,
                    "actual_name": "PulseCoderTemp_1_path1_T_B_OP195A",
                    "last_update_time": 1662514230,
                    "value": 53,
                    "status": 2
                    }
                ]
                }
            ],
            "params_group_status": [
                1,
                1,
                1,
                1,
                1,
                1,
                1,
                1,
                1,
                1,
                1,
                1,
                1,
                1,
                1,
                1,
                1
            ]
            }
    ```

    Explanation for the response body is given below

    ```json

        {
            "param": "This is the id of the parameter group in the parameter group table",
            "param_actual_name": "Actual name of the parameter group",
            "machines": [
                {
                "name": "Name of the machine",
                "status": "Status of the machines, 1 - ok, 2-warning, 3-critical",
                "axes": [
                    {
                    "name": "Axis Id",
                    "actual_name": "Actual name of the parameter as mentioned in the mongodb",
                    "last_update_time": "The recent most time when the parameter was updates",
                    "value": "Value of the parameter",
                    "status": "status of the axis/parameter"
                    }
                ]
                }],
            "params_group_status": "List of length 17 with values either 1, 2 or 3 denoting the
                            summary of status of all machines in that paramter group"
        }
    ```

1. **/api/v1/{machineName}/{parameterGroupId}/{axisId}** - This end point is used to get the real time data for a given machine, parameter group and axis.the given parameter group (such as encoder temperature).

    - **Input Parameter**
        - **machineName** - This is the name of the machine as recorded in the machines table.

        - **parameterGroupId** - This is the id column from the table ParameterGroup to identify the parameter group this parameter belongs to (For example id 4 for group encoder temperature).

        - **axisId** - This is the id as given in the machines axis translation file.

    - **Response Body** - The response body will consist of dictionary of two important key values, the first one denotes the real time data and second one denotes the timestamp of those data.

    ```json

        {
            "param": 4,
            "axis": 0,
            "machine": "T_B_OP160",
            "start_time": 1662512183000,
            "stop_time": 1662512303000,
            "data": [
                36,
                37,
                36
            ],
            "timestamps": [
                1662512183000,
                1662512243000,
                1662512303000
            ],
            "critical_limit": 60,
            "warning_limit": 50
            }
    ```

    Explanation for the response body is given below

    ```json

        {
            "param": "This is the id of the parameter group in the parameter group table",
            "axis": "Axis Id",
            "machine": "Machine name",
            "start_time": "The start time of the returned data in epoch format",
            "stop_time": "The end time of the returned data in epoch format",
            "data": "List of real time data values",
            "timestamps": "List of timestamps in epoch format for the above data points",
            "critical_limit": "The critical limit value for this parameter",
            "warning_limit": "This is the warning limit value for this parameter"
        }
    ```

1. **/api/v1/{machineName}/alarms** - This end point is used to get the summary of alarms for a given machine between given start and end time.

    - **Input Parameter**
        - **machineName** - This is the name of the machine as recorded in the machines table for which alarm summary is requried.

        - **startTime** - This is the start time in epoch format for which a summary of the alarms is requried.

        - **endTime** - This is the end time in epoch format for which a summary of the alarms is requried.

    - **Response Body** - The response body will consist of dictionary of three important key values, the first one denotes alarm count data and second one denotes the total timespan of alarms, third one denotes the timeline data for the alarms between the given start and end time.

    ```json

        {
            "data": {
                "count_data": [
                {
                    "message": "EMBEDDED ETHERNET ERROR DETECTION",
                    "total_count": 122
                },
                {
                    "message": "PMC ALARM",
                    "total_count": 1
                }
                ],
                "timespan_data": [
                {
                    "message": "EMBEDDED ETHERNET ERROR DETECTION",
                    "total_time": 353688.5
                },
                {
                    "message": "PMC ALARM",
                    "total_time": 5
                }
                ],
                "timeline_data": [
                {
                    "enddate_epoch_time": 1655101839,
                    "update_epoch_time": 1655093313.5,
                    "message": "EMBEDDED ETHERNET ERROR DETECTION"
                },
                {
                    "enddate_epoch_time": 1653279888.5,
                    "update_epoch_time": 1653279883.5,
                    "message": "PMC ALARM"
                }
                ]
            }
        }
    ```

    Explanation for the response body is given below

    ```json

        {
            "data": {
                "count_data": [
                {
                    "message": "The alarm message",
                    "total_count": "The total number of times this alarm occured during the given time"
                }
                ],
                "timespan_data": [
                {
                    "message": "The alarm message",
                    "total_time": "The total number of seconds this alarm occured during the given time"
                }
                ],
                "timeline_data": [
                {
                    "enddate_epoch_time": "The enddate time of this alarm as mentioned in the mtlinki mongodb",
                    "update_epoch_time": "The updatedate time of this alarm as mentioned in the mtlinki mongodb",
                    "message": "The alarm message"
                }
                ]
            }
        }
    ```

#### Post End Points

These are end points used to create new data.

1. **/api/v1/{machineName}/{sparePart}** - This end point is used to create new spare part for a machine.

    - **Input Parameter**
        - **machineName** - This is the name of the machine as recorded in the machines table for which new spare part needs to be created.

        - **sparePart** - This is the name of the spare part that needs to be created for this machine.

        - **referencePartNumber** - This is the reference part number (which is equivalent to the part number for the machine when the new part is created or the part count when reset button is pressed). This is used to get the relative part count for the specific spare part. For example if new spare part called "spare part 1" is created when the total part count of the machine is 1000, the reference part number would be 1000, if the total part count for the machine is increased to 1001, then the part count for this spare part would  be 1 (calculatd by subtracting the reference part count for the spare part from the total part count of the machine, 10001 - 1000 = 1 in this case)

        - **warningLimit** - This is the warning limit for this spare part.

        - **criticalLimit** - This is the critical limit for this spare part.

    - **Response Body** - If the creation of new spare part was succesful it returns the (same) input parameters that were given by the client.

    ```json

        {
            "id": 1,
            "part_name": "Spart Part 1",
            "reference_part_number": 100,
            "warning_limit": 1000,
            "critical_limit": 1500,
            "machine_id": 2,
            "count": 0
        }
    ```

    Explanation for the response body is given below

    ```json

        {
            "id": "This is the row id in the spare parts table in the postgresql",
            "part_name": "The spare part name",
            "reference_part_number": "This is the referecen part number",
            "warning_limit": "Warning limit for this spare part",
            "critical_limit": "Critical limit for this spare part",
            "machine_id": "This is the row id corresponding to the machine in the machines table in postgresql",
            "count": "This is the current part count for the spare part, initially it would be zero"
        }
    ```

#### Put End Points

These are end points used to update existing data.

1. **/api/v1/{machineName}/{sparePart}** - This end point is used to update an existing spare part for a machine.

    - **Input Parameter**
        - **machineName** - This is the name of the machine as recorded in the machines table for which new spare part needs to be created.

        - **sparePart** - This is the name of the spare part that needs to be created for this machine.

        - **parameterName** - This is shows which parameter we want to update for the spare part, it could either be reference part number, warning limit or critical limit.

        - **parameterValue** - This is the parameter value.

    - **Response Body** - If the spare part was succesful updated it returns the parameters that were given by the client during the creation of the spare part.

    ```json

        {
            "id": 1,
            "part_name": "Spart Part 1",
            "reference_part_number": 100,
            "warning_limit": 1000,
            "critical_limit": 1500,
            "machine_id": 2,
            "count": 10
        }
    ```

    Explanation for the response body is given below

    ```json

        {
            "id": "This is the row id in the spare parts table in the postgresql",
            "part_name": "The spare part name",
            "reference_part_number": "This is the referecen part number",
            "warning_limit": "Warning limit for this spare part",
            "critical_limit": "Critical limit for this spare part",
            "machine_id": "This is the row id corresponding to the machine in the machines table in postgresql",
            "count": "This is the current part count for the spare part, initially it would be zero"
        }
    ```

1. **/api/v1/parameters_limit/{machineName}/{parameterGroupId}}/{axisId}** - This end point is used to update the warning /critical limits for the static parameter or to set new or update(append) reference signal for dynamic parameter.

    - **Input Parameter**
        - **machineName** - This is the name of the machine as recorded in the machines table whose parameter limits is to be set/updated.

        - **parameterGroupId** - This is the id column from the table ParameterGroup to identify the parameter group this parameter belongs to (For example id 4 for group encoder temperature).

        - **axisId** - This is the id as given in the machines axis translation file.

        - **setType** - This is shows what parameter that the client is trying to set, it could be warning_limit, critical_limit, reference_signal.

        - **limit** - This is the limit value.

        - **append** - This tells if the client is trying to append new reference signal to existing reference signal (value should be true), or replace the existing reference signal with new signal (in this case the append parameter should be false). This is applicable only if the setType is reference_signal.

    - **Request Body** - This is a list of reference signal values, for example : [1, 2, 5, 8]

    - **Response Body** - If the limits are sucessfully updated, it return the set type and value.
    ```json

        {
            "set_type": "warning_limit",
            "value": 55
        }       
    ```

    Explanation for the response body is given below

    ```json

        {
            "set_type": "The parameter set type",
            "value": "The set value for the parameter"
        }       
    ```

#### Delete End Points

These are end points used to delete data.

1. **/api/v1/{machineName}/{sparePart}** - This end point is used to delete an existing spare part for a machine.

    - **Input Parameter**
        - **machineName** - This is the name of the machine as recorded in the machines table for which a spare part needs to be deleted.

        - **sparePart** - This is the name of the spare part that needs to be deleted for this machine.

    - **Response Body** - If returns a message regarding the success or failure of the operation.

    ```json

        {
            "detail": "Successfully Deleted",
            "spare_part": "Spart Part 1"
        }
    ```

    Explanation for the response body is given below

    ```json

        {
            "detail": "Information whether the deletion was successful or not",
            "spare_part": "Spart Part name"
        }
    ```

### Security Route

These set of end points consist of all the routes requrired for security related operations.

#### Post End Points
These are end points used to post data.

1. **/api/v1/auth** - This end point is used to login a user and give JWT token for the session.

    - **Request Body**

    ```json

        {
            "username": "The user name",
            "password": "The user's password"
        }
    ```

    - **Response Body**

    ```json

        {
            "access_token": "eyJhbGiIsInR5cCI6IkpXVCJ9.ey6gH9RWI5D5PFjI",
            "token_type": "bearer"
        }
    ```    

    Explanation for the response body is given below

    ```json

        {
            "access_token": "The JWT token",
            "token_type": "token type"
        }
    ```

1. **/api/v1/register** - This end point is used to register a new user, this can be done only be admin users.

    - **Request Body**

    ```json

        {
            "username": "new_user",
            "email": "new_user@mail.com",
            "full_name": "User Name",
            "password": "password"
        }   
    ```

    - **Response Body**

    ```json

        {
            "username": "user name",
            "email": "email id of user",
            "full_name": "Full name of user"
        }
    ```  
