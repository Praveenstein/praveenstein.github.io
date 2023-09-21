# Collector

## Introduction

The collector consist of scripts to collect data from all different data sources at TIEI, such as general purpose cnc machines, spm machines such as laser cladding, journal grinding. It consist of 4 separate collector services:

- **Static Parameter Collector** - This is used to collect data for static parameters

- **Dynamic Parameter Collector** - This is used to collect data for dynamic parameters

- **SPM Parameter Collector** - This is used to collect data for SPM machines
    
    - **Laser Cladding** - This is used to collect data from laser cladding machines

    - **Journal Grinding** - This is used to collect data from Journal Grinding machines

- **Part Count Monitor/Collector** - This is used to collect part count from all machines.


## Static and Dynamic Collector

### Project Requirement

The requirements for the collector services are:

1. pandas~=1.4.2

1. pymongo~=4.1.1

1. psycopg2~=2.9.3

1. pgcopy~=1.5.0

1. yagmail~=0.15.277

1. scipy~=1.8.1

1. XlsxWriter~=3.0.3

1. numpy~=1.23.0


### Project layout

The following layout shows the general project structure for the Static and dynamic parameters (59 cnc machines) collectors.

    main_static_collector.py            # The main entry point for the static collector service.
    main_dynamic_collector.py           # The main entry point for the dynamic collector service.
    main_report_sender.py               # The main entry point for the report generation service.
    collector_app/
        database/                       # This python package consist of modules related
                                        # to database.
            __init__.py                 # The Initialization file for the python package.
            crud_operations.py          # This python module consist of functions to help
                                        # in database CRUD operations.
            db_utils.py                 # This python module consist of utility functions
                                        # to help in timescaledb operations.
            common_query_templates.py   # This python module consist of template for common queries.
        exception_handling/             # This python package consist of modules related
                                        # to exception handling.
            __init__.py                 # The Initialization file for the python package.
            custom_exception_classes.py # This python module consist of classes for custom
                                        # exception handling classes.
        anomaly_detection/              # This python package consist of modules for the
                                        # anomaly detection.
            __init__.py                 # The Initialization file for the python package.
            detection_algorithm.py      # The file consist of function to do Kruskal–Wallis test.
        collector_classes/              # The package consist of modules that has collector classes.
            __init__.py                 # The Initialization file for the python package.
            collector_classes_module.py # The consist of core python classes that collect data.
        report_manager/                 # The package consist of modules that for report generation.
            __init__.py                 # The Initialization file for the python package.
            email_Sender.py             # The consist of functions to generate reports for abnormality.
        utils/                          # The package consist of utility modules
            __init__.py                 # The Initialization file for the python package.
            config_helper.py            # The consist of functions to help in configuration
                                        # Such as logger configuration, database configuration
            exception_handling.py       # The file consist of function for exception handling
            global_variables.py         # The file consist of function to return some common
                                        # Global variables.
        __init__.py                     # The Initialization file for the python package.


The core functionalities for the collector services are implemeted in the collector classes, namely:

1. **ParametersGroupBase** - This is the class to represent the static parameter group such as encoder temperature. These have specific variables and methods to collect data from the *MtLinki.L1SignalPoolActive* for all the static parameters. These classes inherit from the *ParametersGroupAbstract* abstract class.

1. **DynamicParameters** - This is the class to represent the dynamic parameter group such as spindleload. These have specific variables and methods to collect data from the *MtLinki.L1SignalPool* for all the dynamic parameters. These classes inherit from the *ParametersGroupBase* class, but have specific methods for the requriements of dynamic parameter.

1. **CollectorClass** - This is the class that has variable and methods to use the *ParametersGroupBase* to represent the static parameters and orchestrate the collection of all static parameter group data.

1. **DynamicCollectorClass** - This is the class that has variable and methods to use the *DynamicParameters* to represent the dynamic parameters and orchestrate the collection of all dynamic parameter group data.

The UML class diagram for the above classes are given the diagram below:


``` mermaid
classDiagram
  ParametersGroupAbstract <|-- ParametersGroupBase
  ParametersGroupBase     <|-- DynamicParameters
  CollectorClass          <|-- DynamicCollectorClass
  ParametersGroupAbstract : +String group_name
  ParametersGroupAbstract : +String mongodb_query
  ParametersGroupAbstract : +Int warning_limit
  ParametersGroupAbstract : +Int critical_limit
  ParametersGroupAbstract : +Float latest_update_time
  ParametersGroupAbstract : +Float _temp_latest_update_time
  ParametersGroupAbstract : +String parameter_type
  ParametersGroupAbstract : +Pandas DataFrame recent_data
  ParametersGroupAbstract : +Pandas DataFrame next_alert_time_for_all_signals
  ParametersGroupAbstract : +Pandas DataFrame new_alerts
  ParametersGroupAbstract : +check_for_new_data()
  ParametersGroupAbstract : +get_new_data()
  ParametersGroupAbstract : +add_condition_columns()
  ParametersGroupAbstract : +insert_to_timescaledb()
  ParametersGroupAbstract : +check_for_new_anomaly()
  ParametersGroupAbstract : +send_alerts()
  class DynamicParameters{
    +check_dynamic_condition()
  }
  ParametersGroupBase     <-- CollectorClass:has static parameter
  DynamicParameters       <-- DynamicCollectorClass:has dynamic parameter
  class CollectorClass{
    +String read_cycle_time
    +String static_parameters
    +String dynamic_parameters
    +int combined_alerts
    +load_parameters()  
    +do_workflow()  
    +merge_alerts()  
    +send_combined_alerts()  
    +start_collector()  
  }
```

## Special Purpose Machines

For all the spm machines, the pc which has the log files, is connected to the linux server through network, and the directory is continously monitored for new log files.
As soon as a new file is generated, the services will read them and transforms the data to the timescaledb format and inserts them.

### Project Requirement

The requirements for the laser cladding collector services are:

1. numpy==1.22.3
1. pandas==1.4.2
1. pgcopy==1.5.0
1. psycopg2==2.9.3
1. python-dateutil==2.8.2
1. pytz==2022.1
1. six==1.16.0

### Project layout

The following layout shows the general project structure for all the SPM collectors.

    main.py                             # The main entry point for the laser cladding collector.
    app/
        database/                       # This python package consist of modules related
                                        # to database.
            __init__.py                 # The Initialization file for the python package.
            crud_operations.py          # This python module consist of functions to help
                                        # in database CRUD operations.
            db_utils.py                 # This python module consist of utility functions
                                        # to help in timescaledb operations.
        data_transformation_Service/    # This python package consist of modules related
                                        # to functions that does transformation of log files to 
                                        # Database format.
            __init__.py                 # The Initialization file for the python package.
            transformation_functions.py # This python module consist of function to do log file
                                        # File transformation.
        file_system_operation/          # This python package consist of modules for the
                                        # directory monitoring.
            __init__.py                 # The Initialization file for the python package.
            directory_monitoring.py     # The file consist of function to monitor the machine for 
                                        # New log files.
        initialization_services/        # The package consist of modules that has collector classes.
            __init__.py                 # The Initialization file for the python package.
            initial_setup.py            # The consist of functions to do initial set up of this service.
        utils/                          # The package consist of utility modules
            __init__.py                 # The Initialization file for the python package.
            check_mount.py              # The consist of functions to check if the machine is
                                        # Mounted as a connected device to the linux server
            config_helper.py            # The file consist of function for configuration such as log, database
            input_getter.py             # The file consist of function to get input from the command line
        __init__.py                     # The Initialization file for the python package.

