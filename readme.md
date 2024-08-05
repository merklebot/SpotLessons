# How to work with Spot from Boston Dynamics

- [Lesson 1: Draw your name's first letter with robot's head](./Lesson1/material.md)
- [Lesson 2: Get to know your robot state](./Lesson2/material.md)
- [Lesson 3: Make first steps](./Lesson3/material.md)
- [Lesson 4: Explore the world around you](./Lesson4/material.md)
- [Lesson 5: Spot's mapping](./Lesson5/material.md)
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

## Play via agent's terminal
1. Register at app.merklebot.com
2. Create Organization and open it
3. Add robot in Robots tab, open it and share API key with teacher
4. Create new Robot for your device
5. Install robot-agent with command in robot description. It will look like:
```bash
curl -s https://app.merklebot.com/install.sh | bash -s YOUR_DEVICE_API_KEY
```
6. Install robot-agent CLI with 
```bash
pip install rn-cli
```
7. Add environmental variable AGENT_SOCKET_PATH with socket. By default it is:
```bash
export AGENT_SOCKET_PATH=/merklebot.socket 
```
8. Add job with spot container. Teacher will share json with you
```bash
rn jobs add JSON.json ROBOT_KEY
```

9. Connect to terminal of robot
```bash
rn jobs terminal ROBOT_KEY JOB_ID
```
