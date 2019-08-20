
ST0324 Internet of Things CA2 Step-by-step Tutorial

SCHOOL OF DIGITAL MEDIA AND INFOCOMM TECHNOLOGY 
SmartWH (Smart Warehouse)
=============

IOT CA2 SmartWH
Step-by-Step Tutorial
ST0324 Internet of Things (IOT)

#### Table of Contents
- Section 1 Overview of SmartWH
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


## Section 1 Overview of SmartWH
##### A.  What is SmartWH about?
SmartWH is our interpretation of a smart warehouse. It has everything you need to monitor and maintain a warehouse. Our goal was to make a comprehensive system to monitor and protect a technologically advanced warehouse. The warehouse has an RFID card reader, a temperature and humidity sensor, a burglar alarm, 

##### B. Final Raspberry PI Setup
This is what the final setup should look like.

*insert image of final setup*

##### C. System Architecture Diagram
This is the system architecture diagram of our program.

*insert image of SAD*

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

The Sound Sensor reads the room's ambient sound level. We use this sensor to 

------------

##### 1 HC-SR04 Sensor

![](https://www.makerlab-electronics.com/my_uploads/2016/05/ultrasonic-sensor-HCSR04-1.jpg)

The HC-SR04 Sensor is used as a parking sensor. It reads the distance of the car to the sensor and if the car gets too close, it will display a message on the LCD screen.

------------

##### 1 LED

![](https://www.taydaelectronics.com/media/catalog/product/cache/1/image/500x500/9df78eab33525d08d6e5fb8d27136e95/a/-/a-1554.jpg)

We use this LED to show if access is granted when the RFID Card is tapped. The LED lights up when the authorized card is tapped. It does not light up when the unauthorized card is tapped.

------------

##### 2 LCD

![](https://www.dnatechindia.com/image/cache/catalog/16x2-alphanumeric-display-green-buy-india-500x500.jpg)

We use one LCD to display the authorized card holder's information when tapped.

We use the other LCD to display a message when the distance sensor recognises that the car is too close.

------------

##### Resistors
###### 1 330Ω Resistor

![](https://storage.googleapis.com/stateless-www-faranux-com/2017/03/330-ohm.jpg)

Resistor for the LED
###### 1 10KΩ Resistor

![](https://i.ebayimg.com/images/g/~OEAAOSwA3dYeQl6/s-l300.jpg)

Resistor for the DHT11 Sensor

------------

##### RFID / NFC MFRC522 Card Reader Module

![](https://mundialcomponentes.com.br/arquivos/produtos/imagens_adicionais/304eb202af63065ab456a07af402ac31d13d9599.jpeg)

We use this card and card reader as an authorization checkpoint.

------------


## Section 3 Hardware Setup
In this section, we will connect all the necessary components described in Section 2.

##### Fritzing Diagrams
