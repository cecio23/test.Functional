# IoT Data Edge Consolidation GE - Cepheus #

* [Introduction](#introduction)
* [Testing environment](#testing-environment)
* [Overall preliminary setup](#overall-preliminary-setup)
* [Testing step by step](#testing-step-by-step)


## Introduction ##

IoT Data Edge Consolidation GE - Cepheus is the FIWARE GE by Orange available at its [GitHub repository](https://github.com/Orange-OpenSource/fiware-cepheus).

[Top](#iot-data-edge-consolidation-ge---cepheus)

## Testing environment ##

The testing environment can be easily set up through a FIWARE Lab, which is based on the cloud operating system OpenStack. 
In order to test this GE, two Virtual Machines you needed, which are: 

1. **IoT Data Edge Consolidation GE - Cepheus** - follow the instruction to [deploy a dedicated GE instance based on an image](https://catalogue.fiware.org/enablers/iot-data-edge-consolidation-ge-cepheus/creating-instances ).
2. **Orion Context Broker GE** - follow the instruction to [deploy a dedicated Orion instance](https://catalogue.fiware.org/enablers/publishsubscribe-context-broker-orion-context-broker/creating-instances).
3. **JMeter** - select "base_ubuntu_14.04" image in the FIWARE Cloud Portal to install JMeter on Ubuntu Virtual Machine.


[Top](#iot-data-edge-consolidation-ge---cepheus)

## Overall preliminary setup ##

Once the HW necessary for the test described previously at **Testing Environment** chapter has been setup, the following preliminary steps need to be accomplished before to start the test process:

### 1. IoT Data Edge Consolidation GE - Cepheus ###

> No actions

Open the **/etc/hosts** file by using this command:

> `sudo nano /etc/hosts` 

and add Orion IP of previous VM with **orion** alias according to your instance: 

> `192.168.111.29 orion`

### 2. Orion Context Broker ###

> No actions

Current Orion version 1.7.0.

### 3. JMeter ###

Open the **/etc/hosts** file by using this command:

> `sudo nano /etc/hosts` 

and add Cepheus and Orion IPs of previous VMs with **cepheus** and **orion** aliases according to your instance: 

> `192.168.111.28 cepheus`

> `192.168.111.29 orion`


Copy in the **/tmp/** folder the **Cephus-1.0.0.jmx** file.


#### Install JMeter 3 (on Ubuntu 14.04) ####

1. `sudo apt-get update` - to refresh packages metadata
2. `sudo apt-get install openjdk-7-jre-headless` - Java 7 is pre-requisite for JMeter 3.0
3. `wget -c http://ftp.ps.pl/pub/apache//jmeter/binaries/apache-jmeter-3.1.tgz` - download JMeter 3.1
4. `tar -xf apache-jmeter-3.1.tgz` - unpack JMeter

[Top](#iot-data-edge-consolidation-ge---cepheus)

## Testing step by step ##

**Run the test** with the follow command: 

`./apache-jmeter-3.1/bin/jmeter -n -t /tmp/Cepheus-1.0.0.jmx`

**Retrieve the results** of JMeter session test once it has ended. They are collected in a **csv file** which is placed in the same folder where you are using the jmx file and named as following: 

`cepheus-1.0.0_yyyy-MM-dd HHmmss.csv`

To test that data are in the Orion, please use this command:

> `curl -v http://orion:1026/v2/entities`

An example of result, in json formant, is:

`{"id":"Floor1","type":"Floor","temperature":{"type":"double","value":"19.444444444444443","metadata":{}}},{"id":"Floor2","type":"Floor","temperature":{"type":"double","value":"20.11111111111111","metadata":{}}},{"id":"Floor3","type":"Floor","temperature":{"type":"double","value":"21.666666666666668","metadata":{}}}`

[Top](#iot-data-edge-consolidation-ge---cepheus)