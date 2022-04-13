# Controlling a Motor

To start controlling a motor, lets create a new `Test` subsystem in the `subsystems` package.

![Create Class](../assets/createclass.png)

```java
public class Test extends Subsystem {

    public Test(HardwareMap hardwareMap) {

    }
}
```

To create the motor object, we will use the [DcMotorEx](http://ftctechnh.github.io/ftc_app/doc/javadoc/com/qualcomm/robotcore/hardware/DcMotorEx.html) interface. It's a good habit to declare devices using the `private` and `final` keywords unless they need to be mutated or accessed outside of the class.

```java
private final DcMotorEx motor;
```

In the constructor, we will use `hardwareMap` to initialize the object and specify the device name in the FTC Driver App configuration. Feel free to specify a different device name than `"test"`.

```java
public Test(HardwareMap hardwareMap) {
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
public class Test extends Subsystem {
    private final DcMotorEx motor;

    public Test(HardwareMap hardwareMap) {
        motor = hardwareMap.get(DcMotorEx.class, "test");
    }

    public void setPower(double power) {
        motor.setPower(power);
    }
}
```


Thats all! You can now call the subsystem method in a TeleOp or [create a command](/ftc/create-command) and [add it to a `ButtonBinding`](/ftc/create-binding).
