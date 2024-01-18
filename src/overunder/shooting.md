# Shooting

## Semster 1
For the first semester of the 23-24 Over Under VEX season, we used a catapult to throw triballs over the center bar, used in both skills and match loading for the robot. The catapult was made with a slip gear and a ratchet to make sure that it did not move backwards. When the slip gear was hit by the gear controlling the actual catapult, rubber bands pulling the catapult towards the gear took control, and shot the catapult forwards with the triball, throwing the triball over the center barrier about 50% of the time.

The issues with this design were that the number of rubber bands put excessive stress onto the bars that were holding the catapult and gear on place, and eventually caused enough wear and tear on the gears that were running that catapult that it would be better to replace it. Additionally, during mtch loading and skills, the design of the catapult made it so that it was very easy to drop the triball into the holding area, forcing double possession if holding another triball for us.

## Semester 2

We decided to replace the catapult with a flywheel design for the second semester of our Over Under season. On our [PTO system](./pto.md), we have a pneumatic setting that redirects power to a gear with another chain gear on the same shaft. The chain gear transfers power through chain to a shaft on the [lift](./lift.md), where other gears transfer the power over to the flywheel, using a gear ratio of large to small in order to optimize for the fastest speed possible, shooting as far from the loading location. This design solves the issue of thee tribaaalls dropping into the loading zone and getting stuck, forcing double posession. On the flip side though, the flywheel takes a lot of torque to run and so has a much slower startup time and greater energy consumption that the catapult.
