# Creating a Command

To start, let's create a new `TestCommand` class in the `commands` package and extend the `Command` class. We'll also be using the `TestSubsystem` class from the [previous example](/ftc/control-motor).

<p align="center">
  <img src="../assets/createclasscommand.png" />
</p>

```java
public class TestCommand extends Command {

    public TestCommand() {

    }

    @Override
    public void execute() {

    }

    @Override
    public boolean isFinished() {

    }
}
```

You may notice that I override two methods from the `Command` class, `execute` and `isFinished`. The `execute` method gets called on every loop until `isFinished` returns true. We're going to be using these methods to specify what we want our command to do and when we want it to end. By default, `isFinished` always returns false. 

For this test command, we just want our test motor to move forward for one second via the `ElapsedTime` timer class. To do that, we first need to define our variables and initialize them in the constructor.

```java
private final TestSubsystem test;
private final ElapsedTime timer;

public TestCommand(TestSubsystem test) {
    this.test = test;
    timer = new ElapsedTime();
}
```

Then, we have our `execute` method move the motor forward.

```java
@Override
public void execute() {
    test.setPower(1.0);
}
```

And to finish it off, we have `isFinished` return true when one second has passed.

```java
@Override
public boolean isFinished() {
    timer.seconds() >= 1.0;
}
```

Your class should now look like this.

```java
public class TestCommand extends Command {
    private final TestSubsystem test;
    private final ElapsedTime timer;

    public TestCommand(TestSubsystem test) {
        this.test = test;
        timer = new ElapsedTime();
    }

    @Override
    public void execute() {
        test.setPower(1.0);
    }

    @Override
    public boolean isFinished() {
        timer.seconds() >= 1.0;
    }
}
```

It's that simple. To bind this command to a button press, check out the [next example with the `ButtonBinding` class](/ftc/create-binding).
