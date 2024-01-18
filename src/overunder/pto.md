# PTO System

The PTO sytem, or a power takeoff system, is essentially a mechanic that transfers power from a motor to different systems as needed. In our case, we control the movement of power from the motors using gears and pneumetics. We developed this system during the second semester of the Over Under season.

The PTO system is powered by two motors, connected to a gearshaft at the bottom with a sliding gear controlled by a double action pneumatic, that is positioned horizontally to push a gear into place. to determine whether the gear is powered or not. Depending on the state of the first pneumatic, power is either transferred to the intake or to the lift/shooting mechanism.

The second double action pneumatic right above the first one controls whether the power input goes to the [4 bar(lift)](./lift.md) or the [flywheel(shooting)](./shooting.md), by connecting a gear to a gearshaft if active or retracted. The gearshaft connected then transfers the power to the subsystem using it. Using these two, we have 4 possible configurations to transfer power to subsystems. Since only 3 subsystems need power from the PTO system, the 4th potential case is left unnacounted for in the codebase.
