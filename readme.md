# How to work with Spot from Boston Dynamics

- [Lesson 1: Draw your name's first letter with robot's head](./Lesson1/material.md)
- [Lesson 2: Get to know your robot state](./Lesson2/material.md)
- Lesson 3: Make first steps
- Lesson 4: Explore the world around you (TBD)
- Lesson 5: Spot's mapping (TBD)
- Lesson 6: Robot on duty: missions (TBD)

## Play with our robot

To access our robot, we propose you to schedule session here (**TODO** add link)

Connection to robot's terminal are conducted through app.merklebot.com platform:
1. Register at app.merklebot.com
2. Create Organization and open it
3. Add robot in Robots tab, open it and share API key with teacher
4. Launch Docker Job with next parameters:
   1. Docker image: `ghcr.io/merklebot/spot-lesson-image:master` 
   2. Custom command: `sh`
   3. Network mode: `host`

5. Open the job from Robot **Jobs List** and click `Open Terminal`
6. In opened terminal you can work with code via nano editor. Use the following command to manipulate code:
   1. create program file - `nano main.py`
   2. save - <kbd>CTRL + X</kbd> , <kbd>Y</kbd> , <kbd>ENTER</kbd> 
   3. run - `python3 main.py`