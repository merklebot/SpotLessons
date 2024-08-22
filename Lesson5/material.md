# Lesson 5 - Spot's mapping

## Intro

This lesson discuss some specific mechanics of mapping related to Spot

## Theory

Service, responsible for navigation called `GraphNav`. As it follows from the name, it uses graphs - waypoints and edges, to move Spot around.
To build such map, you'll need to:

1. Start right in front of AprilTag. It will be used as some synchronizing ground truth.
2. Move around your space (the more stable and full of object it is the better the map)
3. Periodically, create waypoint, which will connect to the previous one with edge
4. End the movement
5. Optimize the map with some additional edges

After all this steps you could save your map and use it to move around waypoints. 

>[!Note]
>Path between waypoints goes via edges. If map do not contain some edges, Spot won't go through unknown.

It's quite complicated to write code for this from scratch. We recommend you to use (and explore code) of examples by Boston Dynamics:
1. [GraphNavCommandLine](https://github.com/boston-dynamics/spot-sdk/tree/master/python/examples/graph_nav_command_line) - to build map and move with it
2. [GraphNavMapViewer](https://github.com/boston-dynamics/spot-sdk/tree/master/python/examples/graph_nav_view_map) - to visualize map

## Practice

1. Download BosDynSDK
```bash
git clone https://github.com/boston-dynamics/spot-sdk.git
```
2. Go to GraphNameCommandLine example
```bash
cd ./spot-sdk/python/examples/graph_nav_command_line
```
3. Check the instructions of example, run map recorder. Record the map
4. Run map navigation and enjoy walking
5. Download map to your device, install sdk and run map viewer


## Conclusion

During this lesson you have:
- used Spot's mapping service
- wrote your own map
- moved around it
- visualized surroundings of Spot

> [!TIP]
> It is strongly recommended to look through example's code of navigation. It could be used in more serious usecases