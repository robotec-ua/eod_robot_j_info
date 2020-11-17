# EOD Model J by Robotec

<p align="center">
  <img src="https://github.com/robotec-ua/eod_robot_j_info/tree/main/doc/images/model.png" />
</p>

The remote-controlled explosive ordnance disposal (EOD) robot is designed to provide enhanced bomb disposal capabilities to EOD teams.

The robot offers high reliability and excellent maneuverability. It can be used to identify and disarm booby traps, fireworks, improvised, explosive devices and other dangerous objects in closed areas, buildings and vehicles. It also performs reconnaissance, monitoring and investigation of objects in exceptionally dangerous conditions.

The EOD robot system is in service with military and law enforcement units of more than 41 countries worldwide.

## Project structure
* [Demine robot overview](#overview)
* [Description of techologies](#state_of_art_technologies)
    * [Open-source software](#software_description)
        * [Navigation](#navigation)
        * [Motion system](#motion)
        * [Object recognition](#neural_networks)
        * [Sensor data processing](#system_of_sensors)
    * [Robot's internals](#hardware)
* [Assembling the robot](#assembling)
    * [Creating the details](#robot_details)
    * [Putting everything together](#assembling_instructions)
    * [Wiring it up!](#connecting_the_hardware)
* [Installation guide](https://github.com/robotec-ua/demine_robot_h_install)
* [When everything is done]()
    * [Starting the robot](https://github.com/robotec-ua/demine_robot_h_launch)

## Overview


## State of art technologies
A robot can't be created without advance in technologies.

### Software description
Success of a robot depends on hardware and software in equal ratio : high-quality hardware can't show the best performace without a well-planned, structured and fast software nor good software can be used properly on outdated hardware. So, the team of software engineers in Robotec did their best to create a powerful, simple and scalable software to bring evolution in the world of robotics. 

#### Navigation
Precise navigation is one of the most difficult problems to solve in robotics. There are a lot of different types of navigation and they can achieve different levels of precise movement. Model H is dedicated to complete dangerous tasks, so precision of the robot movements are critical. 

Having that in mind, it was decided that Model H will be equipped with high-precision encoders (tracking position of the robot "on the spot") and modern GPS antenae (to use it with GNSS RTK packages, which is advanced satelite-based technology of highly-accurate navigation).

All the data are fuzed with EKF ([Extended Kalman Filter](https://en.wikipedia.org/wiki/Kalman_filter)), which is dedicated to get and predict inertial system state using noisy or inaccurate data from different sources (GPS and encoders mentioned above). This solution tends to be a lot more accurate than estimation on every of the data separately and is commonly-used in robotics. 

#### Motion
Robots have to do complete different types of tasks and a lot of them require very high precission (in comparison with capabilities of a mere human) and siplicity. Model H has to move itself in spece precisely and predictable, correct itself during "journeys". There are a lot of packages to achieve that goal, but almost all of them required complicated planning and a lot of computing power. Because of that, Robotec used open-source package [move_basic](https://github.com/UbiquityRobotics/move_basic) in their robots. Such choice has a lot of benefits : the package is quite simple yet powerful, it can create a simple trajectory (much less errors while moving),has a reliable and fast obstacle detection system. 

Robotec became a contributor to the package and based [their own](https://github.com/robotec-ua/robotec_move_basic) on it. Now, a good package's become great.

#### Neural Networks
Object detection is not a trivial task for computers, so our robot uses powerful computation module Nvidia Jetson Nano (created for AI appliance), a set of cameras and cutting-edge technology Mask-RCNN to detect mines with accuracy up to 90% on a real-time video. It can detect mines even in motion (2 m/s or 4.47 mph).

The detection module consist of two different parts :
* Filtering
* Detection

Before video can be processed to detect objects on it, it should be filtered to decrease the load of the main computatioal unit, electricity consumption and increase the speed of detection and making a decision. The problem is solved by [filtering package](https://github.com/robotec-ua/robotec_image_filtering), simple yet powerful tool, created by Robotec specialists with scalability and speed in mind.

After filtering, the detection process kicks in. In order to train the network, our team proprocessed and labeled a lot of pictures. Training and testing were performed in order to ensure a high level of accuracy. And we succeded.

Because Mask-RCNN package is a standalone project, imcompatible with our main system, Robotec started the development of a new reliable package, that could be "a man in the middle" between the fast NN technology and Robotec software. As a result, [object detection package](https://github.com/robotec-ua/robotec_mrcnn) was built : widely-applicable highly-configurable and open-source package will be community-driven and always up-to-date.

#### System of Sensors
Nowadays robots can be smart enough to make decisions on their own : where to stop, which of details to get etc. Such a technology couldn't be possible without variety of sensors (analogue to human's senses). And Robotec uses a lot of sensors in their robots to make every possible work done precisely as planned.

To get data from the robot's sensors, specialists in Robotec developed a reliable ROS [package](https://github.com/robotec-ua/robotec_sensor_processing), which can be used to communicate with other devices using variety of protocols (can be easily implemented). The technology is based on using a standalone board powered with STM32 microcontroller, which is connected to every sensor present in the system, reads their state and sends data to the main board using a simple yet reliable protocol (designed especially for appliance in Robotec robots). 

High speed, stability, error-checking capabilities, scalability are the key features of the sensor system in Robotec robots.

### Hardware
The list of the robots "internals" is shown below :
* `NVidia Jetson Nano` - powerful analogue to the famous Raspberry Pi with powerful GPU (with CUDA cores for AI-based appliance)
* `STM32F103C6T8 aka Blue Pill` - popular programmable solution from STMicroelectronics (powerful 32-bit microcontroller with modern intrefaces) 


## Assembling


### Robot details


### Assembling Instructions


### Connecting the Hardware

