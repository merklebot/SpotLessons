# How to work with Spot from Boston Dynamics

- [Lesson 1: Draw your name's first letter with robot's head](./Lesson1/material.md)
- [Lesson 2: Get to know your robot state](./Lesson2/material.md)
- [Lesson 3: Make first steps](./Lesson3/material.md)
- [Lesson 4: Explore the world around you](./Lesson4/material.md)
- [Lesson 5: Spot's mapping](./Lesson5/material.md)
- Lesson 6: Robot on duty: missions (TBD)

## Schedule lesson
Schedule lesson [here](https://cal.com/greatestparrot/schedule-lesson-with-spot) or email at arseniy@merklebot.com

## Play with our robot

To access our robot, we propose you to schedule session here (**TODO** add link)

Connection to robot's terminal are conducted through app.merklebot.com platform:
1. Follow [instruction](https://hackmd.io/6CvIVFTUTaCNfF2ngdqjIA) and create robot 
2. Share your public key and robot private one with teacher
3. Launch Docker Job with next parameters:
   1. Docker image: `ghcr.io/merklebot/spot-lesson-image:master` 
   2. Custom command: `sh`
   3. Network mode: `host`

5. Connect to the robot terminal
6. In opened terminal you can work with code via vim editor
