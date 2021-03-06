# Cnos Restapi Module
Performs restapi operations from a remote server on devices running Lenovo CNOS.

## Synopsis
This module performs restapi operations on a device running CNOS. The Restapi operations retrieve, modify and create resources on the CNOS device. 
It provides a way to manage CNOS devices remotely from server.

## Options

parameter | required | default | choices | Description
:------:  | :------: | :------:| ------ | :------:
outputfile|  yes     |  null   |   []   | This specifies the file path to which the output of each command execution is persisted. Responses from the device are saved here. Usually the location is the results folder. But your user can choose which ever path he has write permission. 
host      |  yes     |  null   |   []   | This is the variable which used to look into /etc/ansible/hosts file so that device IP addresses on which this template has to be applied is identified. Usually it specifies the ansible keyword {{ inventory_hostname }} which is specified in the playbook which is an abstraction to the group of network elements that need to be configured.
username  |  yes     |  null   |   []   | Configures the username to use to authenticate the connection to the remote device. The value of  username is used to authenticate the REST session. The value has to come from inventory file ideally; you can even enter it as variable.
password  |  yes     |  null   |   []   | Configures the password to use to authenticate the connection to the remote device. The value of password is used to authenticate the REST session.The value has to come from inventory file ideally you can even enter it as variable.
use_ssl   |  no     |  True   |[True,False]  | Transport layer used by the RESTAPI. False value indicates http  plaintext communication over port 8090. True value indicates https secured encrypted communication
urlpath   |  yes     |  null   |   []         | URL Path of the RESTAPI
method    |  yes     |  null   |[GET,PUT,POST]| The HTTP method of the request.  GET is typically used for querying objects. POST is typically used for creating/querying objects. PUT is typically used for modifying objects
jsoninp   |  no     |  null   |   []         | Input JSON dictionary. Used by POST, PUT method to input request parameters

## Examples
The following are examples of using the module cnos_restapi. These are written in the main.yml file of the tasks directory. 
```sh
- name: Configure BST feature using a JSON string
  cnos_restapi:
    host: '{{ inventory_hostname }}'
    username: '{{ username }}'
    password: '{{ password }}'
    outputfile: "./results/test_restapi_{{ inventory_hostname }}_output.txt"
    use_ssl: True
    urlpath: /nos/api/cfg/telemetry/bst/feature
    method: PUT
    jsoninp: '{"collection-interval": 20, "send-async-reports": 1,
             "send-snapshot-on-trigger": 1, "trigger-rate-limit": 1,
              "async-full-report": 0, "trigger-rate-limit-interval": 11,
              "bst-enable": 1}'

- name: Fetch BST feature using a JSON string
  cnos_restapi:
    host: '{{ inventory_hostname }}'
    username: '{{ username }}'
    password: '{{ password }}'
    outputfile: "./results/test_restapi_{{ inventory_hostname }}_output.txt"
    use_ssl: True
    urlpath: /nos/api/cfg/telemetry/bst/feature
    method: GET

- name: Fetch BST feature using a JSON string
  cnos_restapi:
    host: '{{ inventory_hostname }}'
    username: '{{ username }}'
    password: '{{ password }}'
    outputfile: "./results/test_restapi_{{ inventory_hostname }}_output.txt"
    use_ssl: True
    urlpath: /nos/api/info/telemetry/bst/congestion-drop-counters
    method: POST
    jsoninp: '{"req-id" : 1, "request-type" : "port-drops", "request-params": {"interface-list": ["Ethernet1/1", "Ethernet1/2", "Ethernet1/3"]}}'

```

## Return Values
On successful execution, the method returns an string with the following message in JSON format: 
"RESTAPI [GET,PUT,POST]  urlpath is successful"

Upon any failure, the method returns an error display string.

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

