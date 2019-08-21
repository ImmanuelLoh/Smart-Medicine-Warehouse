
ST0324 Internet of Things CA2 Step-by-step Tutorial

SCHOOL OF DIGITAL MEDIA AND INFOCOMM TECHNOLOGY 
SMW (Smart Medicine Warehouse)
=============

IOT CA2 SmartWH
Step-by-Step Tutorial
ST0324 Internet of Things (IOT)

#### Table of Contents
- Section 1 Overview of SMW
- Section 2 Hardware requirements
- Section 3 Hardware setup
- Section 4 Create a "Thing"
- Section 5 DynamoDB Setup
- Section 6 AWS EC2 Hosting of Web Application
- Section 7 Reading RFID/NFC Tags Setup
- Section 8 Program Setup
- Section 9 Web Interface Setup
- Section 10 Expected Outcome
- Section 11 References


## Section 1 Overview SMW SMW
##### A.  What is SmartWH about?
SMW is our interpretation of a smart medicine warehouse. It has everything you need to monitor and maintain a medicine warehouse. Our goal was to make a comprehensive system to monitor and protect a technologically advanced warehouse. The warehouse has an RFID card reader, a temperature and humidity sensor, a burglar alarm, a login page, a remotely controllable light, and a parking lot.

##### B. Final Raspberry PI Setup
This is what the final setup should look like.

![](https://i.ibb.co/mNpBrbK/DSC-0135.jpg)

##### C. System Architecture Diagram
This is the system architecture diagram of our program.

![](https://i.ibb.co/9n5YmgB/System-Architecture-Diagram.jpg)

##### D. How the Web Application looks like

*insert images of web application (all pages)*

## Section 2 Hardware Requirements
##### A.  Hardware Checklist
###### 1 DHT11 Sensor

![](https://potentiallabs.com/cart/image/cache/catalog/new%20components/DHT11-800x800.jpg)

The DHT11 Sensor reads the room's temperature and humidity. We use this sensor to get the values of the room's temperature and humidity.

------------



###### 1 Sound Sensor

![](https://imgaz.staticbg.com/thumb/large/oaupload/banggood/images/1C/80/94db0a4e-61fa-4dc6-9533-83a7d301a016.JPG)

The Sound Sensor reads the room's ambient sound level. We use this sensor to trigger the buzzer as part of a burglar alarm.

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

![](https://i.ibb.co/0jHvyPX/IOT-andre-fritzing.png)

![](https://i.ibb.co/gtY11Zd/IOT-thara-fritzing.png)

![](https://i.ibb.co/pZNn9f5/IOT-immanuel-fritzing.png)

------------



## Section 4: Create a "Thing"
a) First, navigate to IoT Core within the AWS website by clicking on services, then IoT Core.

![](https://i.ibb.co/6rNMDfF/CAT-1.png)

Under manage, select things and choose register a thing

![](https://i.ibb.co/XsNvj38/CAT-2.png)

Choose Create a single thing.

![](https://i.ibb.co/Hd6whJy/CAT-3.png)

d) Enter a name for your thing, for example, Smart. Leave the rest of the fields by their
default values. Click next.




e) Click create certificate. After a few seconds, the following page will appear. Download all
four files. As for the root CA, download the VeriSign Class 3 Public Primary G5 root CA
certificate file.



f) Once done, rename the four files accordingly.



g) Move these four files into a directory in the raspberry pi.

h) Click activate.



i) Click register thing. You will create a policy later.



j) Navigate to policies under the secure section. Click create a policy.



k) Enter a name for your policy, for example, SmartParkPolicy and enter the following under
Add statements


l) Navigate to certificates under secure section. Select the certificate you created previously,
and click attach policy. Attach the policy you created previously.

![Alt text](https://github.com/Revanus/DISMIoTSmartParkV2Assignment/blob/master/README%20images/image034.png "Optional title")

![Alt text](https://github.com/Revanus/DISMIoTSmartParkV2Assignment/blob/master/README%20images/image035.png "Optional title")

m) Select the certificate you created previously again, and click attach thing. Attach the policy
you previously created. Attach the thing you created previously.

![Alt text](https://github.com/Revanus/DISMIoTSmartParkV2Assignment/blob/master/README%20images/image036.png "Optional title")
