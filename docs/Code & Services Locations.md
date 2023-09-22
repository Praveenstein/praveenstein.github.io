# Code & Services Location

## Introduction

This section shows the code locations and some of the services names and locations.

## Code Locations

### Collector Services

1. **Static Collector**

    - Code Location

            /home/tnga_iot/iiot_project/codes/collector_system/main_codes/collector_main_2/collector_main/main_static_collector.py

    - Service Name

        static_collector

    - Service File Location (systemctl daemon file)

            /lib/systemd/system/static_collector.service

1. **Dynamic Collector**

    - Code Location

            /home/tnga_iot/iiot_project/codes/collector_system/main_codes/collector_main_2/collector_main/main_dynamic_collector.py

    - Service Name

        dynamic_collector

    - Service File Location (systemctl daemon file)

            /lib/systemd/system/dynamic_collector.service

1. **Laser Cladding Collector**

    - Code Location

            /home/tnga_iot/iiot_project/codes/laser_cladding/laser_clad_main_2/laser_clad_main/main.py

    - Service Name

        laser_cladding_monitoring

    - Service File Location (systemctl daemon file)

            /etc/systemd/system/laser_cladding_monitoring.service

1. **Laser Cladding Collector B**

    - Code Location

            /home/tnga_iot/iiot_project/codes/laser_cladding/laser_cladding_b/laser_clad_main/main.py

    - Service Name

        laser_cladding_monitoring_b

    - Service File Location (systemctl daemon file)

            /etc/systemd/system/laser_cladding_monitoring_b.service

1. **SPM Journal Grinding Collector**

    - Code Location

            /home/tnga_iot/iiot_project/codes/collector_system/main_codes/collector_spm/codes/laser_clad_main/main_2.py

    - Service Name

            journal_grinding_jop_X_collector

    - Service File Location JOP 105 (systemctl daemon file)

            /etc/systemd/system/journal_grinding_jop_105_collector.service

    - Service File Location JOP 130 (systemctl daemon file)

            /etc/systemd/system/journal_grinding_jop_130_collector.service

    - Service File Location JOP 140 (systemctl daemon file)

            /etc/systemd/system/journal_grinding_jop_140_collector.service

1. **Part Count Collector**

    - Code Location

            /home/tnga_iot/iiot_project/codes/collector_system/main_codes/collector_part_count/tiei_main/main_part_count.py

    - Service Name

        part_count_collector

    - Service File Location (systemctl daemon file)

            /etc/systemd/system/part_count_collector.service

1. **Email Sender Service**

    - Code Location

            /home/tnga_iot/iiot_project/codes/collector_system/main_codes/collector_part_count/tiei_main/main_part_count.py

    - Service Name

        email_sender

    - Service File Location (systemctl daemon file)

            /etc/systemd/system/email_sender.service

1. **Summary Repory Generator Service**

    - Code Location

            /home/tnga_iot/iiot_project/codes/collector_system/main_codes/collector_part_count/tiei_main/main_part_count.py

    - Service Name

        report_summary_generator

    - Service File Location (systemctl daemon file)

            /etc/systemd/system/report_summary_generator.service

### Back End Services

The back end in developed in FastApi and deployed as docker container. The codes are available in github and can be downloaded modified and dockerized to make any new changes.


### Front End Services

1. **Apache Server**

The front end is developed using html, css, javascript and react. It is being served by apache server. The codes are available in github and can be downloaded modified and build using node package manager and copied to this location (which the apache server will serve)

    /var/www/tnga_iot