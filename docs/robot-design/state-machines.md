# State Machines

A state machine (or finite-state machine) is defined by two things: states and transitions. A state is simply a way a subsystem should behave, and a transition is an action that changes the state of a subsystem.

![State Machine Diagram](https://m.media-amazon.com/images/G/01/DeveloperBlogs/AppstoreBlogs/default/102117_StateMachine._CB513660882_.png?t=true)
*<center>State machines are abundant everywhere, from vending machines to video games</center>*

Any usage of a subsystem outside of its class is heavily simplified through state machines. For example, controlling an arm is as simple as setting its state to `UP` or `DOWN` and handling the logic in the subsystem. Autonomous programs boil down to setting different subsystem states through commands (explained in the [next section](/robot-design/commands)).

Although state machines are a great way of simplifying logic outside of the subsystem class, it is prone to becoming a method of "sweeping things under the rug" for complex subsystems. Complex subsystem class' can become dense and messy if there are a lot of states, but its often worth the sacrifice in cleanliness for simpler control.

## FTC/FRC Implementations

Both SHPLib and WPILib don't provide state machines built into subsystems due to it being purely user-defined. However, state machines can be easily implemented through enums and transition methods. The example below is an arm subsystem done in the context of FTC, but it can be implemented the same way in FRC.

Within the subsystem class, you can create an enum that contains all of your states and a variable to store your current state. Keep in mind that states depend on the context of the subsystem.

```java
public enum State {
    UP, DOWN, DISENGAGED, RESET
}

private State state;
```

In the constructor, you can set the starting state of the subsystem.

Then, you'll need a method to transition the state.

```java
public void setState(State state) {
    this.state = state;
}
```

Finally, you can handle the state logic in your `periodic` method.

```java
@Override
public void periodic(Telemetry telemetry) {
    switch (state) {
        case UP:
            if (motor.isDisabled()) motor.enable();
            motor.setPosition(3500);
            break;
        case DOWN:
            if (motor.isDisabled()) motor.enable();
            motor.setPosition(0);
            break;
        case RESET:
            motor.resetEncoder();
            // the break statement is purposefully omitted here, allowing the RESET state to both reset the encoder and disable the motor
        case DISENGAGED:
            motor.disable();
            break;
    }
}
```

To learn how to properly use state transitions, check out the [next section on commands](/robot-design/commands).