# Creating a Subsystem

To make a simple subsystem that controls a motor, create a new `TestSubsystem` class in the `subsystems` package and extend the `Subsystem` class.

<p align="center">
  <img src="../assets/createclasssubsystem.png" />
</p>

```java
public class TestSubsystem extends Subsystem {

    public TestSubsystem(HardwareMap hardwareMap) {

    }

    @Override
    public void periodic(Telemetry telemetry) {

    }
}
```

Although we're not going to use the `periodic` method, it's a good habit to override empty methods.

To create the motor object, we will use the [DcMotorEx](http://ftctechnh.github.io/ftc_app/doc/javadoc/com/qualcomm/robotcore/hardware/DcMotorEx.html) interface. It's a good habit to declare devices using the `private` and `final` keywords unless they need to be mutated or accessed outside of the class.

```java
private final DcMotorEx motor;
```

In the constructor, we will use `hardwareMap` to initialize the object and specify the device name in the FTC Driver App configuration. Feel free to specify a different device name than `"test"`.

```java
public TestSubsystem(HardwareMap hardwareMap) {
    motor = hardwareMap.get(DcMotorEx.class, "test");
}
```

Now that the motor is initialized, we need a method to control the motor. Our motor has a method called `setPower` to the power from 1.0 to -1.0 relative to the voltage (1.0 as 100%, 0.0 as 0%, -1.0 as reverse 100%).

```java
public void setPower(double power) {
    motor.setPower(power);
}
```

Your class should now look like this.

```java
public class TestSubsystem extends Subsystem {
    private final DcMotorEx motor;

    public TestSubsystem(HardwareMap hardwareMap) {
        motor = hardwareMap.get(DcMotorEx.class, "test");
    }

    public void setPower(double power) {
        motor.setPower(power);
    }

    @Override
    public void periodic(Telemetry telemetry) {

    }
}
```


Thats all! You can now call the subsystem method in a TeleOp or [create a command](/ftc/create-command) and [add it to a `ButtonBinding`](/ftc/create-binding).
