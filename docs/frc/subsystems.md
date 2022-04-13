# Subsystems

## Drivetrain

### 2022

We used a standard 6 wheel drivetrain with 4 Falcon 500s. Although tank drive is the common for teams with 6 or 4 wheel drive, we decided to use arcade drive to simplify the inputs for the driver. Velocity control, odometry, and kinematics was implemented, but we ran out of time to use it for the autonomous.

[Drive Subsystem Class](https://github.com/SHP-Robotics/2144-FRC2022/blob/master/src/main/java/frc/robot/subsystems/Drive.java)

## Intake

### 2022

The intake was a straightforward over-bumper roller intake controlled by a BAG motor connected to a TalonSRX. We used the intertia from driving the robot to deploy the intake. To bring the intake back into the robot, we had a polyurethane belt winch controlled by a BAG motor connected to a TalonSRX. Because it was relatively simple and heavily intertwined with the indexer, the intake code was kept within the Indexer subsystem.

[Indexer/Intake Subsystem Class](https://github.com/SHP-Robotics/2144-FRC2022/blob/master/src/main/java/frc/robot/subsystems/Indexer.java)

## Indexer

### 2022

The indexer was designed to hold balls in two index positions using beam break sensors. The indexing logic was just logic gates, but it could have been more effective and mutable if split into commands. To move the balls, there was a guide BAG motor with rollers between the intake and the second index position and a polyurethane belt with rollers connected to a Falcon 500 that was responsible for indexing into the first position and feeding into the turret. Because of the beam break logic, there was no need for control loops.

[Indexer/Intake Subsystem Class](https://github.com/SHP-Robotics/2144-FRC2022/blob/master/src/main/java/frc/robot/subsystems/Indexer.java)

## Flywheel

### 2022

The flywheel consisted of two Falcon 500s belted in a 1.0 : 2.5 ratio to the output axle. Velocity control and feedback was done through a combination of a [bang bang controller](/advanced-concepts/control-systems?id=bang-bang-controller) and [feedforward control](/advanced-concepts/control-systems?id=feedforward-control). The bang bang controller was responsible for providing feedback in order to maintain the setpoint while balls were being fed, while the feedforward was responsible for providing static voltage in order to avoid oscillations from the bang bang controller. Units were done in rotations per second.

[Flywheel Subsystem Class](https://github.com/SHP-Robotics/2144-FRC2022/blob/master/src/main/java/frc/robot/subsystems/Flywheel.java)

## Turret

### 2022

The turret itself was a Falcon 500 chained to a lazy susan. The chain was tapped directly into a plate rather than wrapped around a gear, so were were strictly limited to 270 degree movement. Due to the wires, that was reduced to 180 degree movement. In all honesty, the turret logic was thought of on a whim while I was out for a family dinner, but it proved to be extremely effective and flexible. By finding the ratio of TalonFX ticks to turret rotations in degrees, we were able to use a built-in positional [profiled PID controller](/advanced-concepts/control-systems?id=profiled-pid-controller) to accurately adjust the turret angle by degrees.

[Turret Subsystem Class](https://github.com/SHP-Robotics/2144-FRC2022/blob/master/src/main/java/frc/robot/subsystems/Turret.java)

## Vision

### 2022

Vision was pretty straightforward for 2022. We tuned a Limelight 2 to detect the upper hub and used the returned horizontal offset in degrees to adjust the turret. On top of the turret adjustments, we calculated the distance to the hub using the vision measurements and adjusted the flywheel velocity based on an interpolating lookup table.

[Vision Subsystem Class](https://github.com/SHP-Robotics/2144-FRC2022/blob/master/src/main/java/frc/robot/subsystems/Vision.java)

## Arm

## Elevator

## Climber
