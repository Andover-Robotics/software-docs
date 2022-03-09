---
summary: >-
  At one point, we called this "Control Modes". That name might sound more
  intuitive.
---

# Finite State Machines

## Definition

A **Finite State Machine** is a computational pattern where the system is in one of a **finite** number of possible **states** at any moment. For a concrete example, consider the following **state diagram**:

![Simple state diagram for a turnstile (Chetvorno, via Wikimedia Commons)](/assets/image (18).png)

There are two states in this state machine scheme: _Locked_ and _Unlocked_. There are two **events**, _Push_ and _Coin_, that cause the system to enter certain state transitions. Each state has two outward-pointing arrows that each correspond to a particular event: for example, if a user _pushes_ the turnstile when it is _locked_, it will stay locked, according to the leftmost looping arrow; if a user enters a _coin_ when it is _locked_, it will transition to the _unlocked_ state, according to the top arching arrow.

## Application to Robotics

For ARC Thunder's World Championship robot (_"Thor"_), we established an elaborate Finite State Machine in order to facilitate driver operations. In the programming documentation of _Thor_, we included the following state diagram:

![State diagram for Thor's TeleOp](/assets/image (19).png)

Although the events in this state diagram are not shown due to graphical limitations, this diagram demonstrates a clear correlation between the _state_ concept and the operation of a robot during TeleOp. To earn points during the first 90 seconds of TeleOp, _Thor_ performs the following actions repeatedly and in this order:

1. **Collect** minerals from the playing field;
2. **Transfer** collected minerals to the delivery sorter;
3. **Deliver** the sorter to the lander;
4. **Score** points by dropping minerals into the lander.

The four states found near the center of the state diagram reflect the sequential and repetitive nature of this procedure. In _Thor_'s TeleOp scheme, each state corresponds to a different control scheme for one controller, meaning that moving the same control axis can have different results in different states. This is why we referred to Finite State Machines as **Control Modes** previously—each state is a control mode, there is a limited set of mode transitions, and each mode defines a different control scheme.

## Implementing a Finite State Machine

To represent a Finite State Machine in Java, we need to define all possible **states**, the logic for transitioning between them (**state transitions**), the starting state, and what is executed in each state.

### State Representation

We can naturally represent a finite number of states using an **enum** in Java. Each possible value of the enum corresponds to one possible state. For example, ARC Thunder codified all the possible states of _Thor_ into an enum named `TeleOpState`:

```java
public enum TeleOpState {
  CYCLE_COLLECT, CYCLE_TRANSFER, CYCLE_DELIVER, CYCLE_SCORE, ENDGAME, MANUAL
}
```

Then, in the main TeleOp OpMode, a field named `state` is defined and stores the currently active state.

### State Transitions and Actions

The most basic approach to the concept of state transitions uses a large `switch` statement that executes different code segments depending on the current state. Each `case` of the `switch` statement corresponds to one possible state, applies the control scheme of that state, and can make changes to the current state depending on certain conditions. This `switch` statement is executed repeatedly, so it belongs in the `loop()` method of an iterative OpMode. Consider the following example implementation for the turnstile diagram above:

```java
public abstract class TurnstileSwitch {
  private static enum TurnstileState {
    LOCKED, UNLOCKED
  }

  private TurnstileState state = TurnstileState.LOCKED;

  // Executed repeatedly
  public void loop() {
    switch (state) {
      case LOCKED:
        // Actions in LOCKED
        if (newCoinEntered()) {
          state = TurnstileState.UNLOCKED;
        }
        break;
      case UNLOCKED:
        // Actions in UNLOCKED
        if (newPush()) {
          state = TurnstileState.LOCKED;
        }
    }
  }
  
  abstract boolean newCoinEntered();
  abstract boolean newPush();
}
```

In each iteration of `loop()`, the `switch` statement executes different branches depending on the current state. If the state is `LOCKED` and `newCoinEntered()` returns true, it changes the current state to `UNLOCKED`; if the state is `UNLOCKED` and `newPush()` returns true, it changes the current state to `LOCKED`.
