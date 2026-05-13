---
layout: project
title: Mechatronics Robot Design
description: MAE 3780 Mechatronics
technologies: [Electrical System Design, Mechanical Design, Manufacturing, Systems Testing]
image: /assets/images/robot.JPG
---

# MAE 3780 

<br><br><br><br><br><br>

## Competition Objective

Design and build the electrical and mechanical systems for a robot to collect more blocks than an opponent robot operating in the same arena.

<br>

## Our Design

The primary goal of this design is maximizing passive block collection, as opposed to defensive or offensive strategies. The main goal in our block collecting strategy was to quickly collect more than half of the blocks and leave the board. An image of our final robot design is shown below.

<br>

<div style="text-align: center;">
  <img src="{{ '/assets/images/robot.jpg' | relative_url }}"
       alt="Final Robot"
       style="max-width: 85%; height: auto; border-radius: 10px;">
</div>

<br><br>

---

# Mechanical Design

<br>

<div style="text-align: center;">
  <img src="{{ '/assets/images/robot_isometric.png' | relative_url }}"
       alt="Final Robot Isometric CAD"
       style="max-width: 85%; height: auto; border-radius: 10px;">
</div>

<br>

<div style="display: flex; justify-content: center; align-items: center; gap: 30px;">

  <img src="{{ '/assets/images/robot_side.png' | relative_url }}"
       alt="Final Robot Side CAD"
       style="height: 320px; width: auto; object-fit: contain; border-radius: 10px;">

  <img src="{{ '/assets/images/robot_front.png' | relative_url }}"
       alt="Final Robot Front CAD"
       style="height: 320px; width: auto; object-fit: contain; border-radius: 10px;">

</div>

<br><br>

### 1. Gear Train
Since the main goal of our robot was to get to the center of the board as fast as possible, we used the mechanical advantage of a gear reduction to maximize speed. We utilized the given small wheels as large gears by laser cutting acrylic adapters that made them into large wheels. They were attached to a gear train that drove our large wheels faster.

<br>

### 2. Deployable Arms + Collector Screen
In order to maximize the collection area, acrylic deployable arms were used in the front of the robot that made use of the 12” diameter bounding cylinder allowed after deployment. A one-way collector screen fashioned from a plastic sheet collects blocks in the front, with pieces attached to both the push bar and the deployable bars.

<br>

### 3. Push Bar
A laser cut acrylic bar is mounted statically to the front of the car via two buttons which are triggered when the robot runs into another robot.

<br><br>

---

# Electrical Design 

<br>

<div style="text-align: center;">
  <img src="{{ '/assets/images/circuit_diagram.png' | relative_url }}"
       alt="Circuit Diagram"
       style="max-width: 85%; height: auto; border-radius: 10px;">
</div>

<br><br>

### 1. Parallel Button
The two buttons are wired in parallel so that a high signal from either will trigger the interrupt to change paths. The buttons are wired with pull-down resistors so that a high signal will trigger when either button is pressed. This will trigger the alternative path for the robot to move backwards.

<br><br>

---

# Software Design

<br>

<div style="text-align: center;">
  <img src="{{ '/assets/images/robot_flowchart.png' | relative_url }}"
       alt="Robot Flowchart"
       style="max-width: 85%; height: auto; border-radius: 10px;">
</div>

<br><br>

### 1. Deployment Sequence
At the beginning of the deployment sequence, both arms drop down via two servos controlled by a 50 Hz PWM signal from Timer1. Arm 1 is connected to servo 1 which is a positional motor set to a fixed angle. Arm 2 is connected to servo 2 which is a continuous rotation servo whose speed and direction are set by a pulse width. The pulse widths were set using Output Compare Registers 1 and 2 (OCR1 and OCR2).

<br>

### 2. Hard-Coded Path
During competition, barring no interruptions from other robots, our robot drives forward to the middle and turns right, ideally collecting just over half of the blocks on the right side of the board. It then continues and drives off the board and stops, since there are no out-of-bounds.

<br>

### 3. Button Interrupt
Additionally, if the robot hits the other robot, our robot has a “push-bar” (consisting of two buttons) attached to the front that triggers an external interrupt. This interrupt causes the robot to reverse off the board and stop, collecting extra blocks as it moves backward as well.

<br><br>

---

# Competition Analysis 

<br>

The robot competed in 6 rounds and ended with a 3-2-1 score for W-L-T. We noticed that the 2 rounds that ended in losses happened because the button-activation that caused the robot to reverse ended in us losing a majority of the blocks we had already collected. This is largely because the plastic one-way-gate we implemented did not work as well as when we had tested it in the lab, so when we reversed over the edge of the board, we ended up losing a significant number of blocks.

<br>

To fix this problem, we unplugged the wires that electrically connected the button to the robot to avoid triggering the robot reversing direction during the competition. This helped us secure 3 wins and 1 tie in the following four rounds.

<br>

In our best round, we collected 12 blocks from the board, which was made possible by the extra area we achieved by using our micro-servos to deploy additional arms and the speed gained by our geartrain. The deployable arms worked as expected during every round of competition, which helped us increase our robot’s perimeter, and the gear-train was mechanically successful so we were able to increase our speed in collecting blocks before other robots got to the center of the board.

<br>

Although we did not advance to the round robin, we are pleased with the mechanical and electrical success of our robot and that we were able to collect a significant number of blocks in 4 out of 6 rounds.

<br><br>

---

# Design Process Reflection

<br>

Throughout the course of this project, our design evolved rapidly and drastically in direct response to our initial testing results. While our main objectives of:

1. Be fast  
2. Collect and retain blocks  
3. Avoid contact with other robots  

remained throughout our design iterations, the method to achieving those goals changed.

<br>

As mentioned in the strategy overview, one of the primary design objectives for our robot was speed. With a faster robot, we could get to the blocks before our opponent. Our initial strategy to achieve faster speeds was to combine the use of larger wheels with an amplified voltage input to the servos via the use of an operational amplifier (op-amp).

<br>

While this idea seemed initially promising, there were a few difficulties that we ran into along the way. Primarily, we found that when trying to connect the output from the op-amp directly to the h-bridge input, the op-amp output voltage would drop in an unexpected way, not providing an amplified voltage as expected. However, there was a bigger problem with our use of an op amp that we had initially missed — the use of additional 9V batteries (such as those needed to power the op-amp) was not allowed per the rules.

<br>

As a result, we decided to pursue a gear train. However, since we decided to pivot our design quite late, we didn’t have the option to purchase servo gears from a company like Pololu, so instead we designed a custom gear train using gear designs from McMaster and created a gear assembly that could be cut from acrylic and could interface with the spare wheels we had to attach the gears to the servo.

<br>

This design change required quite a lot of debugging and testing, and the final version for competition involved us removing the rubber from the wheels to reduce a stall failure mode we were seeing due to our high RPM, low torque gear train.

<br>

The second critical part of our design was the block retaining mechanism, which was a sheet of plastic designed to fold in one direction when the robot was driving over blocks, and was designed to not fold in the opposite direction in order to retain blocks when driving backward. This part of the design didn’t evolve much, as initial testing with popsicle sticks and cardboard demonstrated that our design would be sufficient.

<br>

The last important part of our design was the button feature at the front of the robot. This feature was designed such that if we ran into another robot or obstacle, the robot would simply reverse while retaining the blocks it collected to avoid the other robot.

<br>

This feature took a bit of iterative development. Initially, the button feature was designed as a piece of acrylic attached directly to one button. However, initial testing demonstrated that this button was not stiff enough, and if the acrylic piece was pushed off-axis, the button wouldn’t be triggered.

<br>

As a result, we improvised and switched to using two buttons attached to the one piece of acrylic to increase the stability of the component and to ensure the button would be triggered upon contact. Due to the fact that we wanted our “drive backward” interrupt to be triggered when either button was pressed, we tried to implement the use of an OR gate component. However, following some issues wiring the component, we decided to get around it by wiring the button outputs in parallel.