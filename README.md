# CanSat
## Ground Station System, CanSat On board Telemetry system with GY-80, Arduino and Xbee


### Ground Station: 

The system was developed pn python 2.7, implements **OpenGL** , **pygame** , **MatplotLib** and [Drawnow](https://github.com/stsievert/python-drawnow )

Firstly, the program reads 20 values from the sensor in order to calibrate it. 

![alt text](https://github.com/AldaCL/CanSat/blob/master/Screenshots/calibration.png)

The data sent by the sensor (Arduino / Xbee), make up an array of 15 values for different sensed magnitudes, in order, these are:
* Temperature (In Fahrenheit degrees)
* Presure (Raw pressure, its converted to Pa)
* Altitue (Absolute OSL , with calibration we get height)
* Pitch, Roll, Yaw (Absolute magnitudes, its converted to degrees over calibration position)
* Heading Filtered 
* Kalman Pitch, Kalman Roll; Get after apply kalman filter. 
* Acceleration (X, Y ,Z), Got from Accelerometer
* Gyro (X, Y , Z), Got from Gyroscope. 

Feel free to ignore some magnitudes and use only those that are useful for your purposes< you only need to comment the lines on Arduino code and in python code; also change the size of array to receive. 

Once the sensor was calibrated, it start to receive the meseaurements, at a 19200 baud rate; (Also can be modified, in orden to ajust to your needs, but once again remeber to change this value in arduino code)
![alt text](https://github.com/AldaCL/CanSat/blob/master/Screenshots/ejec1.png)

A few moments after, the MatplotLib window come up, and shows the plot of data (We only take Temp, pressure, Altitude and height)

![alt text](https://github.com/AldaCL/CanSat/blob/master/Screenshots/can2.png)
![alt text](https://github.com/AldaCL/CanSat/blob/master/Screenshots/can3.png)

And the 3D model of Cansat.

![alt text](https://github.com/AldaCL/CanSat/blob/master/Screenshots/can1.png)
![alt text](https://github.com/AldaCL/CanSat/blob/master/Screenshots/can4.png)


We use the values of Pithc, roll and yaw to emulate the movement of the satellite; Axis were changed from original ones; because of the position of sensor into the CanSat. 


Arduino Script take libraries from [Korneliusz Jarzębski](https://github.com/jarzebski) repositories, just added to libraries dir to facilitate integration.

On ground, Xbee is connected to a Arduino UNO to provide Serial comunication with the Laptop USB port. 
a Xbee Shield can be utilized, but due to the ease of getting an Arduino UNO, it was implemented with this. 

### On board telemetry system: 

The on telemetry system on satellite is conformed by an Arduino nano, GY-80 Sensor and a Xbee S2C pro RF Module working at 900 MHz.

Arduino code reads values from sensor via I2C, then send it to XBee  Module connected. 

![alt text](https://github.com/AldaCL/CanSat/blob/master/Screenshots/schemat.png)

Xbee Module send data via RF to Xbee module in ground. (I strongly recommend research about Xbee protocol, configuration ,operation frequency, antenna gain and path losses effects because it define the maximun length of your communications system). 

Our configuration could reach a maximum distance of 600 m with LOS. At this distance any object in the path can cause loss of communication.

### On Mision results: 

