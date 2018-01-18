# ansible-role-cnos-telemetry
CNOS Telemetry Role for support of Lenovo's CNOS-based networking devices in Ansible

## Overview

* Module provides access CNOS Restapi for switch management functions.
* Python Script to generate telemetry roles based on user input

## Requirements

* Ansible 2.4 installed.  [Ansible Installation Instructions](http://docs.ansible.com/ansible/intro_installation.html)
* Lenovo CNOS network device version 10.5 or later
* Restapi Feature enabled on switch

## Documentation

### Python Script to generate telemetry roles based on user input

The python script *tlmreport.py* creates telemetry roles based on user input. It creates commands, results, template, tasks and vars sub-directory, populating the tasks and the variable in the tasks and variable directory respectively. 

The script is executed using the python.
"python tlmreport.py"

#### User input Description

##### rolename
      The ansible rolename to be used in the playbook. A directory is created with the rolename with the commands, results, template, tasks 
      and vars sub-directory. 
##### Controller IP
      The IP address of the controller which receives the telemetry data from the switch. 
##### Controller Port
      The controller's TCP listening port that receives the telemetry data from the switch. 
##### Controller Vrf
      The vrf of the configured IP address. This value is either management or default
##### Heart beat interval 
      The switch sends a heartbeat to the configured controller every few seconds. The heartbeat interval is configured by this    
      parameter. The range is between 1 and 600.
##### Report type 
      The type of telemetry report.
      1 - Predictive Congestion Report 
      2 - Congestion_Detection
      3 - Capacity_Planning
  
  Report Type | Description
  --- | ---
  Predictive Congestion Report | This selection sets thresholds on certain realms. On reaching or exceeding the configured threshold, the switch sends reports to the controller. *Trigger Rate Interval* is the interval when these threshold reports are sent to the controller from the switch. *realm* is the realm that use choose to configure the threshold. The script request user to enter the indexes and the threshold values for the configured realm.
 Congestion_Detection | This selection configures congestion detection reports periodically. There are four types of congestion reports supported. *top-drops* reports the ports experiencing maximum congestion. The number of ports and the periodicity of the report is further required as input for *top-drop* report. *port-drops* reports the port specific congestion.The list of interfaces and the periodicity of the report is further required as input for *port-drop* report. *top-port-queue-drops* reports the port queues experiencing maximum congestion. The number of port queues, the periodicity of the report and queue-type are further requested as input for *top-port-queue-drops* report. *port-queue-drops* reports port queues specific congestion. The list of interfaces, type of queue, periodicity and queue list is further required as input for *port-queue-drops* report.
 Capacity Planning | This selection configures a periodic report of the current realms buffer count. The periodicity of the report is further given as input.
         
### Module and Role Deployment
 Download the zip or tar.gz file containing and unzip into local directory.
 
## License

* GPLv3
* Copyright (C) 2017 Lenovo, Inc.
