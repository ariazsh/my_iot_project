# Photoresistor - datatransfer to cloud

**Ariaz Shafiiyon (as227pd)**

## Tutorial on how to send data from photoresistor to Pybytes

The aim of this project is to experiment with IoT devices and gain more knowledge about the subject. I have chosen to create a photoresistor that uploads the light sensor values every 10 seconds to the Pybytes cloud platform through Message Queuing Telemetry Transport (MQTT). For this project Pycome expansion board is used together with FiPy and a photoresistor and resistor that is connected to though pins and breadboard. The software for the project is written in MicroPython inorder to communicate with the FiPy.  

The estimated time to recreate this project is approximately 3-5 hours. 

### Objective

This project was an assignment from the course 22ST - **1DT305 - Applied Internet of Things, Introduction - 7,5 hp**. 

In this project, I chose to build a light sensor device with FiPy that reads an analog value (measuring the light intensity) to then send the data to the cloud. The purpose of this project was to gain more knowledge about how communication between devices (datatransfering) works. An insight i expect to get from this project is how devices communicate with each other (communication protocols) 

### Material 
//TODO: List of material

//TODO: Description

//TODO: Cost and source 


| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

### Computer Setup

To be able to follow the steps in this tutorial, a development enviroment has to be set up. The microcontroller *FiPy* needs an IDE, for instance **Atom**, to read data from the sensors and to able to program it with the programming language *MicroPython*.

#### Step 1 - install Atom as IDE and Node.js

**1. Download Atom from this [link](https://hackmd.io/@lnu-iot/SydH7MTcw), choose the desired OS for your environment and follow the steps (from 1-4). Make sure to install the Pymakr in step 4.**

Pymakr is required to add a REPL console to Atom that connects to your Pycom board.

**2. Install Node.js inorder to use the Pymakr extension in Atom. You can donwload it directly from this [link](https://nodejs.org/en/) - it is recommended to download the Latest Features (Current).**

#### Step 2 - Update Pycom firmware

Make sure that the microcontroller is updated with the latest version. This to ensure that eventual bugs are fixed and the latest libriries are available for the tutorial.

**1. Plug in the FiPy board onto the Pycom expansion board to then connect it, via a USB cable, to your computer.**

**2. Make sure to download the Pycom Firmware Updater. You can follow the steps from this [link](https://hackmd.io/@lnu-iot/SJ91R_jSO).**
 
#### Step 3 - Test the device

Make sure to test your device before uploading your code.

**1. Create a file in Atom, name it 'main.py'**

**2. Copy the code and test the RGB LED lights for the microcontroller into that file and save it.**

**3. Test that your REPL works by entering *2 + 2* and press enter (or ctrl + alt + r) which then should you give you the output *4*.**

**4. If correct output is given, you can upload the code by pressing the upload icon (or ctrl + alt + s).** 

The following program will switch colors between Red, Green and Blue every second. *Note the time.sleep(1)*.

```python
import pycom		# Import pycom to control LED
import time		# Import time to create delays

# We disable LED heartbeat to control it manually
pycom.heartbeat(False)

# Your board run this section over and over
while True:
    #colors in hexadecimal (0xRRGGBB)
    pycom.rgbled(0xFF0000)  # Red
    time.sleep(1)
    pycom.rgbled(0x00FF00)  # Green
    time.sleep(1)
    pycom.rgbled(0x0000FF)  # Blue
    time.sleep(1)
```

### Putting everything together

![Figure 1](https://github.com/ariazsh/my_iot_project/blob/main/bisquit.jpg "Circuit")

**Note** that, when connecting the sensors (photoresistor), make sure to **not** connect the usb to your computer (or a power source). This could lead to damaging the sensors. From Pysense, pins P0 and P1 connects to FiPy P0 and P1, Vin 5V and Ground connect to FiPy 5V and Ground. From FiPy, the pins Ground and 3V3 connect to photoresistor (**Do note that you should not use the 5V to connect to the photoresistor since it can lead to damaging the photoresistor**).    

### Platform

I have chosen to use Pybytes as a platform, which is a cloud platform. [Pybytes](https://pybytes.pycom.io/) is Pycoms official plattform for sending/recieving data from the cloud. The reason I chose this platform is due to that it is easy to setup and mainly because it has built in libraries that makes it easy to connect to the local WIFI. Another advantage with Pybytes is that it is a free platform and thus you do not need to pay to use it. If I had more time on this project, I would experiment with adding more sensors (for instance to measure temperature), and combine platforms by sending data from PyBytes to Datacake.  

### The code

```python
from machine import ADC
from machine import Pin
import time

LightSensorPin = 'P16' # sensor connected to P16. Valid pins are P13 to P20.

lightPin = Pin(LightSensorPin, mode=Pin.IN)  # set up pin mode to input
                                                                                                                            
adc = ADC(bits=10)             # create an ADC object bits=10 means range 0-1024 the lower value the less light detected 
apin = adc.channel(attn=ADC.ATTN_11DB, pin=LightSensorPin)   # create an analog pin on P16;  attn=ADC.ATTN_11DB measures voltage from 0.1 to 3.3v

while True:
    val = apin()
    pybytes.send_signal(3, val)
    print("sending: {}".format(val))
    time.sleep(10)
```
We need three libraries: ADC, Pin and time. The ADC protocol is needed to create an adc object that can represent the light intensity with a value ranging from 0 - 1024. The Pin library is mainly needed for a function that takes two parameters with the pin ID of the light sensor (in our case 'P16') and information about what mode the pin is set to (in our case input). 

In a loop, we store the analog value (*val*) from the photoresistor and send it to the platform Pybytes (signal 3). The value is then printed out in our REPL and a time sleep is set with value 10 seconds (this is where the library *time* is needed).  

### Transmitting the data / connectivity

Data is sent through [*MQTT*](https://mqtt.org/) protocol with *WIFI* connection, since MQTT is designed for IoT networks and known for its reliability of connecting devices to internet and energy-efficiency. The photonsensors send the sensor values every 10 seconds (as described above in **The code** section). This due to a time sleep of 10 seconds so that we can store the values in Pybytes database. 

### Presenting the data

![Figure 2](https://github.com/ariazsh/my_iot_project/blob/main/dashboard.png "Dashboard")

**Figure 2** shows the dashboard where on the left diagram, data is shown for how much data is stored in Pybytes database in the last day. We see that more than 500B was recieved in a sample test. Since the sample test was very small, it is better to observe the results from the right diagram where the time span is smaller (past hour data). Unfortunality, the x-axis of the right diagram is mixing the time and 'pm' text in several web browsers. This makes it difficult to read the x-axis of the right diagram.

![Figure 3](https://github.com/ariazsh/my_iot_project/blob/main/Signal_3.png "Signal_1")

![Figure 4](https://github.com/ariazsh/my_iot_project/blob/main/Signal_3_1.png "Signal_2")

**Figure 3-4** shows some of the photoresistors values recieved in the Pybytes database *every 10 seconds*. In **Figure 3** and **Figure 4** two lower values are shown (351 and 105) where the photoresistor was exposed to less light. The data is automatically saved in Pybytes database. 

### Finalizing the design
//TODO: Show final results of the project

//TODO: Pictures




