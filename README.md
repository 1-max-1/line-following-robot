# line-following-robot

<img src="https://github.com/user-attachments/assets/760177e0-df84-450d-884f-e417c7630840" width="70%">

This robot was constructed and raced in an annual competition for ENMT221. We designed all aspects of the robot including the PCB. The robot did well and achieved 2nd place.
The track consists of a looped black line on a white background. The robot must succesfully follow the line all the way around, and the time taken determines the ranking.

*The design files are not currently available publicly as this is a recurring course assignment.*

### Chassis
The key features of the chassis are:
- Rail allowing adjustable placement of sensor boards
- Batteries mounted underneath PCB to keep the center of gravity low
- Adjustable motor mounts to vary the tension in the rubber bands used to turn the wheels
- Silicone coating on the outside of the wheels for extra grip
We found that a shorter chassis greatly improved the performance of the robot as it was able to make tight turns more easily.

### Electronics
The sensors boards each contain an IR led and sensor. The voltage in the sensing circuit varies with the amount of IR reflected.

The main board has the MCU (`atmega4808`) which reads the information from the sensor boards and decides what to do. The motors are driven with power mosfets.
I made an attempt at creating a mosfet gate driver circuit with an `LM555` timer. Due to the rules, this was the only available chip I could use.
The circuit was intended to switch the mosfet faster with higher current - in theory this would make the system more efficient. The circuit worked but did not provide any noticeable increase in performance.

The motor driver circuit only allowed for the motors to turn in one direction. Designing an h-bridge would be more complex, however motors that spin backwards would have allowed the robot to turn much tighter.

### Software
The information from the sensors was used to determine how far the robot had deviated from the line. Because our circuit used analog values, this produced a relatively continous and accurate result.
This error value is then fed into a PID controller which produces an output used to drive the motors. This output is scaled and capped to ensure the signal to the motors is correct.
