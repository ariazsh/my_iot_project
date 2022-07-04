# Photoresistor - datatransfer to cloud

**Ariaz Shafiiyon (as227pd)**

## Tutorial on how to send data from photoresistor to Pybytes

//TODO: ye aks

### Project overview

//TODO: yekam beskrivning

### Time approximation

//TODO: 2 deighei

### Objective

This project was an assignment from the course 22ST - 1DT305 - Applied Internet of Things, Introduction - 7,5 hp. 

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

//TODO: Circuit diagram (can be hand drawn)

### Platform
//TODO: Describe platform in terms of functionality.

//      etc. Is your platform based on a local installation or a cloud? 

//      Do you plan to use a paid subscription or a free? 

//      Describe the different alternatives on going forward if you want to scale your idea.


### The code

//TODO: import code and explain - reference

### Transmitting the data / connectivity
//TODO: How often is the data sent?

//TODO: Which wireless protocols did you use (WiFi, LoRa, etc …)?

//TODO: Which transport protocols were used (MQTT, webhook, etc …)


### Presenting the data

![Figure 1](https://github.com/ariazsh/my_iot_project/blob/main/dashboard.png "Dashboard")

//TODO: Description of figure 1

![Figure 2](https://github.com/ariazsh/my_iot_project/blob/main/Signal_3.png "Signal_1")

![Figure 3](https://github.com/ariazsh/my_iot_project/blob/main/Signal_3_1.png "Signal_2")

//TODO: Description of figure 1 and 2

//TODO: How often is data saved in the database. => time.sleep(10)


### Finalizing the design
//TODO: Show final results of the project

//TODO: Pictures




