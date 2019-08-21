
ST0324 Internet of Things CA2 Step-by-step Tutorial

SCHOOL OF DIGITAL MEDIA AND INFOCOMM TECHNOLOGY 

SMW (Smart Medicine Warehouse)
=============

IOT CA2 SmartWH
Step-by-Step Tutorial
ST0324 Internet of Things (IOT)

Done by: Immanuel Loh, Tharine Ramachandran, Andre Ching

#### Table of Contents
- Section 1 Overview of SMW
- Section 2 Hardware Requirements
- Section 3 Hardware Setup
- Section 4 phpMyAdmin/MySQL Setup
- Section 5 Create a "Thing"
- Section 6 DynamoDB Setup
- Section 7 SNS Setup
- Section 8 Reading RFID/NFC Tags Setup
- Section 9 Program Setup
- Section 10 Web Interface Setup
- Section 11 Expected Outcome
- Section 12 Video Demonstration
- Section 13 References

## Section 1 Overview of SMW
##### What is SMW about?
SMW is our interpretation of a smart medicine warehouse. It has everything you need to monitor and maintain a medicine warehouse. Our goal was to make a comprehensive system to monitor and protect a technologically advanced warehouse. Not only is this a warehouse, it also contains a smart parking lot. The warehouse has an RFID card reader, a temperature and humidity sensor, a burglar alarm, a login page, a remotely controllable light, and a parking lot.

##### Final Raspberry PI Setup
This is what the final setup should look like.

![](https://i.ibb.co/bbw8V3C/DSC-0133.jpg)

##### System Architecture Diagram
This is the system architecture diagram of our program.

![](https://i.ibb.co/9n5YmgB/System-Architecture-Diagram.jpg)

##### How the Web Application looks like

Login Page
![](https://i.ibb.co/PcGgpYR/webpagelogin.png)

This Login page validates the adminstrator's credentials. This is a security precaution we have taken to protect the webpage which control sensitive information.

Entry Point Page
![](https://i.ibb.co/Pg86K3p/webpageentry.png)

This page displays the number of times an authorized user has tapped their card to enter the warehouse. It displays the data in both a graph and a table.

Warehouse Page
![](https://i.ibb.co/tCG3B1s/webpagewarehouse.png)

The Warehouse page shows the current temperature in the room. The graph and table update every few seconds. The user also has control of an LED.


## Section 2 Hardware Requirements
##### A.  Hardware Checklist
###### 1 DHT11 Sensor

![](https://potentiallabs.com/cart/image/cache/catalog/new%20components/DHT11-800x800.jpg)

The DHT11 Sensor reads the room's temperature and humidity. We use this sensor to get the values of the room's temperature and humidity.

------------



###### 1 Sound Sensor

![](https://imgaz.staticbg.com/thumb/large/oaupload/banggood/images/1C/80/94db0a4e-61fa-4dc6-9533-83a7d301a016.JPG)

The Sound Sensor reads the room's ambient sound level. We use this sensor to trigger the buzzer as part of a burglar alarm if sound is detected.

------------

##### 1 HC-SR04 Sensor

![](https://www.makerlab-electronics.com/my_uploads/2016/05/ultrasonic-sensor-HCSR04-1.jpg)

The HC-SR04 Sensor is used as a parking sensor. It reads the distance of the car to the sensor and if the car gets too close, it will display a message on the LCD screen.

------------

##### 1 LED

![](https://www.taydaelectronics.com/media/catalog/product/cache/1/image/500x500/9df78eab33525d08d6e5fb8d27136e95/a/-/a-1554.jpg)

We use this LED to represent a light that can be controlled via the webpage.

------------

##### 2 LCD

![](https://www.dnatechindia.com/image/cache/catalog/16x2-alphanumeric-display-green-buy-india-500x500.jpg)

We use one LCD to display the authorized card holder's information when tapped.

We use the other LCD to display messages that instruct the car to either park, reverse or stop.

------------

##### Buzzer

![](https://cdn.shopify.com/s/files/1/0176/3274/products/5v-mini-buzzer_1024x1024.jpg?v=1561293769)

We use the buzzer as part of the burglar alarm system. It triggers when sound is detected.

------------

##### Resistors
###### 1 330Ω Resistor
Resistor for the LED
![](https://storage.googleapis.com/stateless-www-faranux-com/2017/03/330-ohm.jpg)


###### 1 10KΩ Resistor
Resistor for the DHT11 Sensor
![](https://i.ebayimg.com/images/g/~OEAAOSwA3dYeQl6/s-l300.jpg)



------------

##### RFID / NFC MFRC522 Card Reader Module

![](https://mundialcomponentes.com.br/arquivos/produtos/imagens_adicionais/304eb202af63065ab456a07af402ac31d13d9599.jpeg)

We use this card and card reader as an authorization checkpoint.

------------


## Section 3 Hardware Setup
In this section, we will connect all the necessary components described in Section 2.

##### Fritzing Diagrams

![](https://i.ibb.co/74YSpJW/IOT-andre-fritzing.png)

![](https://i.ibb.co/gtY11Zd/IOT-thara-fritzing.png)

![](https://i.ibb.co/pZNn9f5/IOT-immanuel-fritzing.png)

------------

## Section 4: phpMyAdmin/MySQL Setup
Login into phpMyAdmin. It can be accessed via “x/phpmyadmin” where x is your RPI IP address.

![](https://i.ibb.co/GsqKDrp/CAT-40.png)


Create a database named “assignmentdatabase” (I am using tempdatabase for demonstration purposes).

![](https://i.ibb.co/mBLjyqp/CAT-41.png)

Create a table in the database named “temperaturerecord” with the values as seen in the image. Tick the box under A_I(Auto Increment) for id.

![](https://i.ibb.co/3kM4cJw/CAT-43.png)

Create a user that is able to access the database with all priorities. Username “assignmentuser” password “robots1234” .

![](https://i.ibb.co/q53wFYs/CAT-44.png)

## Section 5: Create a "Thing"
Firstly, navigate to IoT Core within the AWS website by clicking on services, then IoT Core.

![](https://i.ibb.co/6rNMDfF/CAT-1.png)

Under manage, select things and choose register a thing

![](https://i.ibb.co/XsNvj38/CAT-2.png)

Choose Create a single thing.

![](https://i.ibb.co/Hd6whJy/CAT-3.png)

Enter a name for your thing, for example, SMW. Leave the rest of the fields by their default values. Click next.

![](https://i.ibb.co/YQkyg1f/CAT-4.png)


Click create certificate. After a few seconds, the following page will appear. Download all four files. As for the root CA, click CA1 certificate file. Remember to save it.

![](https://i.ibb.co/pvdb03R/CAT-5.png)

![](https://i.ibb.co/7Qj4fqt/CAT-6.png)

![](https://i.ibb.co/v1Whxhs/CAT-7.png)

Once done, rename the four files accordingly.

![](https://i.ibb.co/19y6PVz/CAT-8.png)

![](https://i.ibb.co/W5Hcb14/CAT-9.png)

Move these four files into a directory in the Raspberry Pi. Click activate.

![](https://i.ibb.co/C9HCHTz/CAT-10.png)

Click attach policy then click register thing. You will create a policy later.

![](https://i.ibb.co/282QNJk/CAT-11.png)

Navigate to policies under the secure section. Click create a policy.

![](https://i.ibb.co/z5wQx0F/CAT-12.png)

Enter a name for your policy, for example, SMWPolicy and enter the following under "Add statements". Click create when done.

![](https://i.ibb.co/kSFW762/CAT-13.png)


Navigate to certificates under secure section. Select the certificate you created previously,
and click attach policy. Attach the policy you created previously.

![](https://i.ibb.co/yhqk8hd/CAT-14.png)

Select the certificate you created previously again, and click attach thing. Attach the policy
you previously created. Attach the thing you created previously.

![](https://i.ibb.co/vBhLzNs/CAT-15.png)

Take note of your Endpoint

![](https://i.ibb.co/QfQWhtn/CAT-16.png)

### Note: You will need to 2 "Things" for this project. One for the RPI with the DHT11 sensor and one for the RPI with the RFID card reader.
------------




### Installing Libraries for "Things"

Run the following command on your Raspberry Pi to install the AWS Python Library

```
sudo pip install --upgrade --force-reinstall pip==9.0.3
sudo pip install AWSIoTPythonSDK --upgrade --disable-pip-version-check
sudo pip install --upgrade pip

```
## Section 6 DynamoDB Setup

#### DynamoDB

First, navigate to DynamoDB within the AWS website by clicking on services, then DynamoDB. Click create table.

![](https://i.ibb.co/x7d67xj/CAT-17.png)

Fill in the data as shown. Click create.

![](https://i.ibb.co/M2d8tLJ/CAT-18.png)

Go to IAM service on AWS Console and click "Roles"

![](https://i.ibb.co/8MpqDdS/CAT-24.png)

Click "Create Role" and on the next page, choose "AWS service", then "IOT". Under "Select your use case", select IoT.

![](https://i.ibb.co/NWG6wv4/CAT-25.png)

 Click "Next" until you are required to input a name for your role.
 
 ![](https://i.ibb.co/v4gXst2/CAT-26.png)

Next, navigate to IoT Core within the AWS website by clicking on services, then IoT Core. Click Act, then click Create.

![](https://i.ibb.co/2Srv0Vm/CAT-19.png)

Enter the data as shown.

![](https://i.ibb.co/8x2kCCL/CAT-23.png)

Then, navigate to "Set one or more actions" and click the "Add action" button under it.

![](https://i.ibb.co/98mZWZJ/CAT-20.png)

Select the second option. Click "Configure action".

![](https://i.ibb.co/7Rbc2qj/CAT-21.png)

Select the table which you have previously created. Click  Select. Select the role you have created previously. Click Add Action, then click Create Rule.

![](https://i.ibb.co/cLp37vg/CAT-27.png)

## Section 7 SNS Setup

In the AWS IoT console, click Test.
Type on the topic on which your thing publishes. 
Click “Subscribe to topic”

![](https://i.ibb.co/7Y6NMC0/CAT-28.png)

Navigate to SNS on AWS Console. Click topics. Then click Create Topic.

![](https://i.ibb.co/mSfqKMw/CAT-29.png)

Type in your topic name. Then click Create topic. Make a note of the ARN for the topic you just created.

![](https://i.ibb.co/NtdB0Dv/CAT-31.png)

Click Subscriptions and then click Create subscription. When directed to this page, fill in the data as applicable and select Email as the protocol.

![](https://i.ibb.co/m01smR3/CAT-32.png)

After confirming your subscription, access the AWS IoT console and choose "Act", then Create. 

![](https://i.ibb.co/n3JfwqW/CAT-33.png)

Enter data as shown.

![](https://i.ibb.co/v3zBQRg/CAT-34.png)

Then, navigate to "Set one or more actions" and click the "Add action" button under it. Select SNS.

![](https://i.ibb.co/Y8Bnx1Y/CAT-35.png)

Choose the Amazon SNS topic you created earlier, choose data type as JSON, and select your role.

![](https://i.ibb.co/SPxBHdV/CAT-36.png)

## Section 8 Hardware Setup


#### Enable SPI and prepare the MFRC522 libraries

If your raspberry pi is not configured with the MFRC522 libraries, you can follow the following
instructions to set it up.

##### << Enable SPI via raspi-config >>


a) Run raspi-config, choose menu item “5 Interfacing Options” and enable SPI.

```
sudo rasp-config
```
![](https://i.ibb.co/2gs0wBm/CAT-38.png)

![](https://i.ibb.co/Qv537By/CAT-37.png)


##### << Enable device tree in boot.txt>>

a) Modify the /boot/config.txt to enable SPI

```
sudo nano /boot/config.txt
```

b) Ensure these lines are included in config.txt

```
device_tree_param=spi=on
dtoverlay=spi-bcm2835
```

**<< Install Python-dev>>**
c) Install the Python development libraries

```
sudo apt-get install python-dev
```

**<< Install SPI-Py Library >>**

d) Set up the SPI Python libraries since the card reader uses the SPI interface
```
git clone https://github.com/lthiery/SPI-Py.git
cd /home/pi/SPI-Py
sudo python setup.py install
```

**<< Install RFID library >>**

e) Clone the MFRC522-python library and copy out the required files to your project directory
```
cd ~
git clone https://github.com/pimylifeup/MFRC522-python.git
cd ~/MFRC522-python
sudo python setup.py install

```

## Section 9 Program setup

The following codes are needed for the application to work.  There are 3 separate RaspberryPIs. Entry Point needs the RFID Codes, Iot Core "Thing", AWS DynamoDB, Rules and Services. Warehouse needs DHT11 Codes, AWS DynamoDB, Rules and Services. The Parking Lot does not need any of these and only requires codes. Remember to execute above steps and ensure that the RPIs have been successfully set up before running the files. The files will be in the zip folder and will not be in the tutorial.

### Installing Necessary Libraries

Install boto3 using the command below.

```
sudo pip install boto3
```

Install the rpi-lcd library using the commands below.

```
sudo pip install rpi-lcd
```

Run this command to install paho-mqtt which AWS is dependant on.
```python
sudo pip install paho-mqtt
```
Install Mosquitto broker and clients to your Raspberry Pi

```python
sudo apt-get install mosquitto mosquitto-clients
```

### Run files

Run rfid.py for Entry Point RPI

```
sudo python rfid.py

```

Run distancesensor.py for Parking Lot RPI

```
sudo python distancesensor.py

```

Run server.py, sound2.py, telegram.py, aws_pubsub_temp.py, tempdata.py for Warehouse RPI.

```
sudo python server.py
sudo python sound2.py
sudo python telegram.py
sudo python aws_pubsub_temp.py
sudo python tempdata.py

```


## Section 10 Web Interface Setup

The following files are required for the web interface to work.

![](https://i.ibb.co/CW6qYSj/CAT-39.png)

The files will not be in the tutorial due to their size. They can be found in the .zip of the project.


## Section 11 Expected Outcome

### Entry Point RPI
Entry Point RPI requires the codes in the RFID folder. When working correctly, it will display a message on the LCD screen when an RFID card is tapped. If the card is not authorized, it will display "Access Denied". If I tap my authorized card it will display a message with my name, "Hello Immanuel". Everytime I tap my authorized card, it will take a picture and send it to AWS. This is a safety measure in place for the warehouse. 

### Parking Lot RPI
Parking Lot RPI requires the codes in the Distance Sensor folder. When working correctly, it will display a message on the LCD screen if a car is too close, far or just nice. If the car is too far, it will display "Reverse". If it the car is too close, it will display "Stop". If the car is in perfect parking distance, it will display "Park".

### Warehouse RPI
The Warehouse RPI requires the codes in the Server, Sound Sensor, Telegram and Temperature folders. When working correctly, the Warehouse RPI will have a webpage, where there will be a graph for the temperature and a graph for the RFID card reader. Both display historical values of the two in a table and a graph. The data captured and displayed is Temperature in °C and number of times the RFID card has been tapped, respectively. There is also a button to remotely control the LED. A telegram bot can be launched. This telegram bot can take a picture of the Warehouse and also control the LED.

## Section 12 Video Demonstration

You can watch us demonstrate and explain the program [here](https://youtu.be/nkdrZ8nbrqc).

## Section 13 References
SP IOT Practicals

Startbootstrap.com. (2019). SB Admin 2 - Start Bootstrap. [online] Available at: https://startbootstrap.com/template-overviews/sb-admin-2/ [Accessed 21 Aug. 2019].
