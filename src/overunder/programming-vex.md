# VEXCode

## [Codebase](https://github.com/calhighrobotics/over_under_b/tree/vexcode-23)

This page goes over the original code written for the 1516B Over Under Season in 2023, where the code was made using the VEXCode framework and was in use primarily during the months of June to December.

## Portions of the program

The portions of the code contain a user control function and a autonomous function, which further contains the rerun function. The rerun function also contains helper functions that are called from both the autonomous and user control functions. So, a visualization of the functions made in the program would be as follows:

```
Helper Functions(Rerun)
User control
- Rerun write call
- Rerun execution time recording
Autonomous control
- Rerun reader call
- Execution and replay of recorder motor values
- Inclusion of sensor values into the calculation of rerun 
```


## Rerun - Autonomous

Essentially, the rerun function records the velocities of the motor encoders as well as the time taken per each execution loop in the user control program. This value is required because the loop execution time is necessary to update the different motor velocities in the autonomous function as they need to be called.

The recorded values are put into a text file. These values of the motor velocities are replayed by simulating a user control loop(in our case, a while loop checking for controller events) and adding a wait time for simulating latency in the user control loop. This wait time has been recorded along with the motor velocities and is accurate to a microsecond level.

The motor encoder values are read and the robot perceives the autonomous program similar to how it would see the control loop, except with predefined instructions.

# User Control

The 1516B user control function uses relatively simple and straightforward checks of controller events inside a controller loop. It also uses a tank drive approach. 

The rerun function recording is called from inside this user controller function, where the latency of the user control loop and motor encoder values are recorded into their appropriate text files.

# Helper Functions

The helper functions for this program are for a variety of tasks, some being serializing data to fit into a certain data type limited by the framework we are using, as well as actually writing to and reading from files to receive usable data for the rerun or another portion of the code.
