LINE FOLLOWER ROBOT USING P CONTROLLER

HARDWARE REQUIRED TO BUILD A LINE FOLLOWER ROBOT :
1.  1 transparent chassis of plastic
2.  4 motors
3.  4 wheels
4.  L298N motor driver board 
5.  ARDUINO UNO
6.  5 TCRT5000 infrared tubs
7.  5 LEDs
8.  5 resistors
9.  1 mini protoboard
10. 2 battery boxes
11. 3 batteries
12. 1 USB cable for Arduino
13. Cables, screws and bolts

Basically, the integer values of transduction are simplified even further by classifying them into 2 bins: 0 (low values) and 1 (high values).
There are 5 TCRT5000 modules. Each TCRT5000 module has an associated semantics, the variable line. Line adds -4, -2, 0, 2, and 4 if the corresponding TCRT5000 modules are active. 
Then line is divided by the number of active TCRT5000 modules because many TCRT5000 modules can be active at once.
For example, 1 or 2 TCRT5000 modules can be active at once. So, the resulting line value is in the range [-4, 4], only integer values are allowed.
If the line value is 0, it means the robot is on track without deviation.
Higher absolute values of line means the robot is deviated and motors must turn the robot in PROPORTION to the variable line.

The Arduino loop has 2 modes of operation:

Mode 1: When 1 or 2 TCRT5000 modules are active at once, it means the robot is not so deviated can correct its course by making small PROPORTIONAL adjustments to its position by 
slowing down one motor at the corresponding side. The command digitalWrite(LED_BUILTIN, HIGH) is executed to visualize this mode.

Mode 2: When no TCRT5000 modules or all TCRT5000 modules are active, it means the robot is seeing background without line.
So, the robot must turn around its own position to the last seen value of the variable line and make no further advancements.
That is, the robot must turn its wheels by activating the pairs of motors in opposite directions. The command digitalWrite(LED_BUILTIN, LOW) is executed to visualize this mode.

The integral part and the derivative part of the PID controller were not required for this project. The integral part was not required because this robot has no drift.
The derivative part was not required because the robot shows no oscillations in its movements.
Proportional adjustments are small enough to avoid oscillations and frequent enough to keep the robot on track.