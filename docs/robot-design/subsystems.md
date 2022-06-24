# Subsystems

When approaching the design of our robot and the way we interface with it in the code, it's important that we break down the robot into different parts, referred to as **subsystems**, to make it easier to work on independent functions of the robot (and avoid [circular dependencies](https://stackoverflow.com/a/38042916)).

![WPILib Subsystem Diagram](https://docs.wpilib.org/en/stable/_images/subsystems-and-commands.drawio.svg)
*<center>Ignore the command diagram for now, that will be explained in the next section.</center>*

This form of abstraction is also referred to as decomposition, a popular programming practice that you'll learn a lot about from KMo in AP Computer Science.

Subsystems can be anything from a drivetrain to an arm, the scope of a subsystem is purely up to you. However, it's important that you don't abstract several different functions of your robot into one subsystem or have a subsystem for only one device (for the sake of demonstration, only one motor is used in the examples).