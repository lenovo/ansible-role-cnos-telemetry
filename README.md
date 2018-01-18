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

BSD 3-Clause License

Copyright (c) 2018, Lenovo
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

* Neither the name of the copyright holder nor the names of its
  contributors may be used to endorse or promote products derived from
  this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
