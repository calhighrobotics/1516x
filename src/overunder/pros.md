# PROS

## [Codebase](https://github.com/calhighrobotics/over_under_b)

Over the break between semester 1 and 2, we decided to migrate our codebase from VexCode into PROS. We did this as we believed that PROS could offer us greater control and innovation opportunities than that of VexCode. As we migrated the codebase, we decided to change some functions in our program from the VexCode version, to suit the newly rebuilt robot made for the second semester of the Over Under season 23-24.

## User Control.

For user control, we implemented a [tank drive](https://wiki.purduesigbots.com/software/robotics-basics/tank-drive) system that would use one joystick to control each side of the drivetrain. It allows for the driver to get better control of each side of the robot and lets the driver perform error correction if a motor somehow fails in the middle of a match.
```cpp
int left = controller.get_analog(pros::E_CONTROLLER_ANALOG_LEFT_Y);
int right = controller.get_analog(pros::E_CONTROLLER_ANALOG_RIGHT_Y);

// std::abs takes the absolute value of whatever it is called on.
// Thus, any values in range (-5,5) are discarded as 0.
if(std::abs(left) < deadzone) {
    left = 0;
}
if(std::abs(right) < deadzone) {
    right = 0;
}

// Drive the left side of the robot forward at joystick left Y speed
drive_left.move(left);
// Drive the right side of the robot forward at joystick right Y speed
drive_right.move(right);
```
Our motors are split into 3 groups, two being the right and left sides of the drivetrain respectively, and the final group being the two motors powering the [PTO](./pto.md) system. The pneumatics are controlled independently but are generally grouped into the PTO pneumatics and the wing pneumatics.

The [PTO](./pto.md) motors are controlled by basic controls that run the motor group on the PTO when the R1 or R2 button is pressed, to go forwards or backwards respectively. The wings are set with a toggle that turns the pneumatics on with a button click and then turns them off if pressed again.

Additionally, a toggler has been implemented that allows the driver to control the subsystem of the PTO with an easier user interface, by toggling through the PTO options. The toggler automatically adjusts the pneumatics to direct power to the subsystem labeled on the controller. The code used to implement this system is under:

```cpp
if(controller.get_digital_new_press(pros::E_CONTROLLER_DIGITAL_X)) {
			if (subsystem == 1) {
				// intake
				controller.clear_line(0);
				pto_1.set_value(false);
				controller.print(1, 0, "System %d : Intake", system);
			}
			if (subsystem == 2) {
				// Four Bar
				controller.clear_line(0);
				pto_1.set_value(true);
				pto_2.set_value(true);
				controller.print(1, 0, "System %d : 4-bar", system);
			}
			if (subsystem == 3) {
				// Flywheel
				controller.clear_line(0);
				pto_1.set_value(true);
				pto_2.set_value(false);
				controller.print(1, 0, "System %d : Flywheel", system);
			}

			subsystem = subsystem + 1;

			// Checks if the toggler goes out of bounds.
			if (subsystem == 4) {
				subsystem = 1;
			}

		}
```

## Autonomous control

For the autonomous period, we mainly focus on using our drivetrain to move the robot to the goal and place a triball in. We have not used our subsystems extensively in the autonomous period due to how unpredictable they could potentially be and how they could leave the robot in a state that is unwanted. Therefore, we are focusing on achieving simple goals and compounding them, such as delivering a triball to the alliance goal zone.

We have a inertial sensor, and use it in coordination with built-in motor encoders for [odometry](https://wiki.purduesigbots.com/software/odometry). We use an [external framework](https://lemlib.github.io/LemLib/) to manage the mathematics and calculations of this function for us. We use the same framework to manage our [pure pursuit](https://wiki.purduesigbots.com/software/control-algorithms/basic-pure-pursuit) path and by extension our autonomous routine. We use [PID controllers](https://wiki.purduesigbots.com/software/control-algorithms/pid-controller) to manage our speeds and ensure that the robot reaches its appropriate goal most of the time.
