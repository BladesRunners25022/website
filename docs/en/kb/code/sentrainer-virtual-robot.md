---
title: Practice with virtual_robot
description: Learn Java for FTC at home, without a robot or Control Hub - the Learn Java for FTC book and the virtual_robot simulator.
---

# Practice with virtual_robot

**Who:** students starting out in Java, or who want to code when the robot isn't available.
**Time:** about 15 minutes of setup.
**Prerequisites:** Git, Android Studio and Liberica JDK 17 *Full* installed, as in [Workstation and first build](poste-et-premier-build.md) (steps 2 to 4).

The robot isn't always around: it's at school, being taken apart, or another group is using it. To learn Java and the FTC SDK anyway, we combine two free tools:

- **[Learn Java for FTC](https://github.com/alan412/LearnJavaForFTC/blob/master/LearnJavaForFTC.pdf){ target="_blank" rel="noopener" }**, the book by Alan G. Smith (free PDF). It teaches Java step by step with a **programming board**: a motor, a servo, a potentiometer, a touch sensor and a color-distance sensor wired to a Control Hub. The [author's GitHub repository](https://github.com/alan412/LearnJavaForFTC) also has the exercise solutions.
- **[virtual_robot](https://github.com/Beta8397/virtual_robot)**, a 2D FTC robot simulator. It includes a **Programming Board** configuration that reproduces the book's board: you do the exercises on your computer, with no hardware.

## 1. Clone virtual_robot

1. In Android Studio: `File` → `New` → `Project from Version Control` (or `Clone Repository` on the welcome screen).
2. URL: `https://github.com/Beta8397/virtual_robot.git`.
3. `Directory`: a folder **next to** the team project, with no spaces or accented characters, for example `C:\ftc\virtual_robot` or `~/ftc/virtual_robot`.
4. `Clone`, then `Trust Project`.

The simulator is a separate project: don't copy the team's code into it, and don't copy the simulator into the team repository.

## 2. Pick the simulator's JDK

1. `File` → `Project Structure` → `Project`.
2. `SDK`: select **Liberica 17**. If it isn't listed: `Add SDK` → `JDK…`, then pick the folder where Liberica was installed.
3. `Language level`: `17`.
4. `Apply`, then `OK`.

## 3. Run the simulator

Click the green arrow (`Main` configuration) in the toolbar. A window opens with the field, the configuration menus and a virtual gamepad.

1. `Configuration` menu: choose **Programming Board**.
2. `Op Mode` menu: choose an OpMode, for example `TestProgrammingBoard`.
3. Use `INIT`, `START` and `STOP` as on the Driver Station.

The board doesn't move around the field, but you can rotate it with the mouse to test the IMU.

## 4. Do the book's exercises

- Write your classes and OpModes in `TeamCode/src/org/firstinspires/ftc/teamcode`, with a `@TeleOp` or `@Autonomous` annotation, extending `OpMode` or `LinearOpMode`, just like on the real robot.
- The simulator's device names are the book's:

    | Device | Name in `hardwareMap` |
    |---|---|
    | Motor | `motor` |
    | Servo | `servo` |
    | Touch sensor | `touch_sensor` |
    | Potentiometer | `pot` |
    | Color-distance sensor | `sensor_color_distance` |
    | IMU | `imu` |

- Restart the simulator (green arrow) after each code change so it picks it up.

## Useful options

??? tip "Use a real gamepad"
    Open `Controller/src/virtual_robot/config/Config.java`, set `USE_VIRTUAL_GAMEPAD` to `false`, plug in the gamepad and run the simulator. Then press `Start` + `A` to make it `gamepad1` (`Start` + `B` for `gamepad2`).

??? tip "Window too big for the screen"
    In `Config.java`, reduce `FIELD_WIDTH` (for example from `648` to `576`) and switch the `BACKGROUND` image to the matching size (the file name ends in `576.bmp`, in `Controller/src/virtual_robot/assets`).

## Limits

- The simulator provides an **approximation of the FTC SDK**: most exercises work, but some advanced APIs may be missing or behave differently.
- It isn't an Android project: no Gradle, no deployment. What works in the simulator must be **checked again on the real Control Hub**.

!!! success "Tested"
    Setup tested and working on Windows with Android Studio Rabbit and Liberica JDK 17 *Full*.

!!! question "To be confirmed"
    Not yet tested on macOS (the author believes Liberica 17 *Full* works there). Feedback welcome: see [Contributing](../contribuer.md).
