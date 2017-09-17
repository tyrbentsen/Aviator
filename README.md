# Aviator AI Autopilot
Aviator is an independent, open AI Autopilot project aiming at enhancing aircrafts and drones with autonomous flying capabilities.

The main structure of the project is summarized here. More details can be found below.

- [ ] Software
    - [ ] Low-level (runtime) stack   
        - [ ] Real-time operating system
        - [ ] Device drivers
        - [ ] IO framework
    - [ ] High-level (application) stack   
        - [ ] Sensing
        - [ ] Planning
        - [ ] Decision making
        - [ ] Control
        - [ ] Health monitoring
    - [ ] Testing   
        - [ ] Software unit testing
        - [ ] Software-in-the-loop testing  
        - [ ] Hardware-in-the-loop testing  
- [ ] Hardware
    - [ ] Embedded development board
    - [ ] Sensors & actuators
    - [ ] Communication bus
    - [ ] Mechanical platform
- [ ] Documentation and website


## Development

### Software

#### Low-level (runtime) stack   
The low-level stack consists of a framework that provides simple IO access for the application layer. It runs on top of a real-time operating system and schedules the execution of the application's tasks, provides input and output with sensors and actuators, as well as manages the communication with other devices over a bus. 

##### Real-time operating system
The operating system is the lowest level software part on which all other software functions will run. A real-time operating system might be needed for tasks that require high speed and deterministic execution times like IO and control. Tasks running at a slower pace (sensing, decision making) don't necessarily need this.

##### Device drivers
Drivers for IO and communication devices are integrated in OS and made accessible through the low-level IO framework.

##### IO framework
This task consist of the development of a framework in Rust that makes abstraction of the underlying hardware and IO devices. The applications tasks will run on top of this framework.

The framework manages the application's state as well as coordinates the input/output between different application tasks and external devices.

The framework monitors the sensor inputs and communication buses. When data is received, it parses this data and converts it to a typed object. The high level task is simply executed as a function call which the typed input data object as function argument. The high level tasks performs its computations and returns an object with the results. The IO framework takes this return data and serializes it back for the required output device / communication bus. The framework takes care of the necessary duplication and error detection of input/output data.

This framework can be compared with web frameworks like Asp.Net, Django, Rails, Node.js which abstract http requests to a series of function calls.


#### High-level (application) stack   
The high level application stack provides the functionality for sensing, planning, decision making and control of the aircraft. 

##### Sensing
Based on sensor data, the state of the vehicle and its environment is deduced. This is a pipeline of computer vision, state estimation, and machine learning algorithms.

##### Planning
Based on the state of the aircraft and its environment, a plan is sought to accomplish the mission goals. Multiple strategies are employed to find multiple alternative plans.

##### Decision making
Based on the available plans, a decision is made regarding the best plan to accomplish the goal. In case of issues, this function also takes care of falling back to an emergency plan.

##### Control
This function guides the aircraft along the path determined in the previous steps. Based on the current state and input of the aircraft, it determines the best control actions to be sent to the actuators.

##### Health monitoring
This function monitors the other tasks, as well as the sensors and actuators, and it checks if components are working correctly. In case of problems, this function tries to deduce the origin of the problem and informs the decision making component on whats going on.


#### Testing   
This project involves many diverse software components. Testing is needed in order to have certainty that everything works as designed. It also speeds up development, since it provides quick feedback on if everything is still ok, after a change to the software.

##### Software unit testing
Unit testing tests the software components individually, which a number of given test cases.

##### Software-in-the-loop testing  
Since this is embeddded software that controls a physical device, we must also test what the effect is of the software on the device and its environment. To this end, models of the aircraft are created, and a simulation is run in which the autopilot software is coupled to a simulation of the aircraft and its environment. Multiple different scenarios can be tested automatically in this way.

##### Hardware-in-the-loop testing  
Same as software-in-the-loop testing, but in this case the software is running on the actual autopilot hardware, and is coupled to a virtual simulation of the aircraft. Sensor data and actuators signals are replaced by their virtual counterpart. With hardware-in-the-loop, errors can be found that originate from the difference in hardware (cpu, 32/64 bit, busses) between the desktop development computer and the embedded computer.


### Hardware

#### Embedded development board
A high performance board on which the main software is run. Smaller dedicated hardware boards might be needed for sensor acquisition and actuator control. Currently no board is selected yet.

#### Sensors & actuators
Different sensors measure inputs. Sensors must be lightweight to be carried on an aircraft or drone. Currently no sensors and actuators are selected yet.

#### Mechanical platform
This platform is the physical base platform that is controlled by the Aviator AI Autopilot. It is the mechanical frame to which is everything is attached. It must have powerfull moters and batteries in order to fullfill its mission. A possible standard controller that might be present, is replaced by the Aviator hardware and software. Currently no platform is selected yet. 


### Documentation and website
Documentation ensures that everyone is one the same page, such that all components are compatible. It also provides a better insight in the assumptions and guarantees that every sub components makes.