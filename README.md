
ST0324 Internet of Things CA2 Step-by-step Tutorial

SCHOOL OF DIGITAL MEDIA AND INFOCOMM TECHNOLOGY 
SMW (Smart Medicine Warehouse)
=============

IOT CA2 SmartWH
Step-by-Step Tutorial
ST0324 Internet of Things (IOT)

#### Table of Contents
- Section 1 Overview of SMW
- Section 2 Hardware Requirements
- Section 3 Hardware Setup
- Section 4 Create a "Thing"
- Section 5 DynamoDB Setup
- Section 6 MQTT Setup
- Section 7 Reading RFID/NFC Tags Setup
- Section 8 Program Setup
- Section 9 Web Interface Setup
- Section 10 Expected Outcome
- Section 11 References


## Section 1 Overview SMW
##### A.  What is SMW about?
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

```python
sudo pip install --upgrade --force-reinstall pip==9.0.3
sudo pip install AWSIoTPythonSDK --upgrade --disable-pip-version-check
sudo pip install --upgrade pip

```
## Section 5 DynamoDB Setup

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

Select the table which you have previously created. Click  Select. Select the role you've created previously. Click Add Action, then click Create Rule.

![](https://i.ibb.co/cLp37vg/CAT-27.png)

## Section 6 MQTT Setup

In the AWS IoT console, click Test.
Type on the topic on which your thing publishes. 
Click “Subscribe to topic”

![](https://i.ibb.co/7Y6NMC0/CAT-28.png)

Navigate to SNS on AWS Console. Click topics.

![](https://i.ibb.co/mSfqKMw/CAT-29.png)

