# Lesson #4 - Explore the world around you

## Intro

This lesson is dedicated to way Spot feel the World around him

## Theory

### Images

The most convenient way to understand what is happening around the robot is to get images from its cameras. By default, Spot has:

- frontleft_fisheye_image
- frontright_fisheye_image
- left_fisheye_image
- right_fisheye_image
- back_fisheye_image

>[!NOTE]
> Images from Spot's cameras have so called fisheye effect. If you want to use them with some pretrained model, you should take note of that

Access to images are provided via `ImageClient`.  It help you to:
1. Get images and write them (even from few sources at the same time)
2. Get access to depth cameras
3. Picture pixel coordinates (x, y) to camera frame coords (x, y, z)
4. Convert depth image to pointcloud

Detailed description of all the methods and functions in Python SDK could be found [here](https://dev.bostondynamics.com/python/bosdyn-client/src/bosdyn/client/image)

### World Objects

World object service provide way to work with external objects such as AprilTag fiducials (something similar to QR codes),
door handles, stairs or some custom virtual objects. 

Among the uses of those objects, fiducials take the most notable place. They could be used as some anchor points, which are required to make robot movement more precise.
To learn more about their shapes and sizes, read an article at [Boston Dynamics Support page](https://support.bostondynamics.com/s/article/About-Fiducials).

Each of objects has it's own coordinate system, to which or from which you could transform to more prefered one's.

Detailed description of all the methods and functions in Python SDK could be found [here](https://dev.bostondynamics.com/python/bosdyn-client/src/bosdyn/client/world_object)


## Practice

Let's start with the images. You will find useful next classes and functions imported:

```python
from bosdyn.client.image import ImageClient, save_images_as_files, write_image_data
```
1. Register `ImageClient` like all the previous clients
2. Get list of all available sources with client method `list_image_sources`
3. Pick few sources and as a list of strings request images (method `get_image_from_sources`)
4. Get the list of Images proto. Save them one by one with `write_image_data` or in batch with `save_images_as_files`


As an example of work with world objects, let's find one fiducial marker and stand right next to it.
You will find useful next classes and functions imported:
```python
from bosdyn.client.world_object import WorldObjectClient
from bosdyn.api import world_object_pb2
from bosdyn.client.frame_helpers import (BODY_FRAME_NAME, VISION_FRAME_NAME, get_a_tform_b, get_vision_tform_body)
import numpy as np
from bosdyn.client.math_helpers import Quat, SE3Pose
from bosdyn.client.robot_command import RobotCommandBuilder, RobotCommandClient, blocking_stand
from bosdyn.client.robot_state import RobotStateClient
```
1. Register `WorldObjectClient` and `RobotStateClient`
2. Check the list of available world objects with `list_world_objects`. To filter only fiducials, use `object_type` param:
```python
response = world_object_client.list_world_objects(object_type=[world_object_pb2.WORLD_OBJECT_APRILTAG])
```
3. Get list of (filtered) objects as `world_object` field of response. And choose required fiducial:
```python
fiducial = response.world_objects[0]
```
4. Prepare coordinate transformation from AprilTag frame to some world (e.g. VISION_FRAME) coords, and get them to
```python
vision_tform_fiducial = get_a_tform_b(
    fiducial.transforms_snapshot, VISION_FRAME_NAME,
    fiducial.apriltag_properties.frame_name_fiducial).to_proto()
```

5. Get fiducial position relative to world
```python
fiducial_rt_world = vision_tform_fiducial.position
```

6. Use following functions to make calculate coordinates and heading for robot at distanation point:
```python
def get_desired_angle(xhat):
    """Compute heading based on the vector from robot to object."""
    zhat = [0.0, 0.0, 1.0]
    yhat = np.cross(zhat, xhat)
    mat = np.array([xhat, yhat, zhat]).transpose()
    return Quat.from_matrix(mat).to_yaw()


def offset_tag_pose(object_rt_world, dist_margin=1.0):
    """Offset the go-to location of the fiducial and compute the desired heading."""
    robot_rt_world = get_vision_tform_body(robot_state.kinematic_state.transforms_snapshot)
    robot_to_object_ewrt_world = np.array(
        [object_rt_world.x - robot_rt_world.x, object_rt_world.y - robot_rt_world.y, 0])
    robot_to_object_ewrt_world_norm = robot_to_object_ewrt_world / np.linalg.norm(
        robot_to_object_ewrt_world)
    heading = get_desired_angle(robot_to_object_ewrt_world_norm)
    goto_rt_world = np.array([
        object_rt_world.x - robot_to_object_ewrt_world_norm[0] * dist_margin,
        object_rt_world.y - robot_to_object_ewrt_world_norm[1] * dist_margin
    ])
    return goto_rt_world, heading

robot_state = robot_state_client.get_robot_state()
pose, heading = offset_tag_pose(fiducial_rt_world, 1)

goal_x = pose[0]
goal_y = pose[1]
```

7. Move to the goal position and heading with `synchro_se2_trajectory_point_command` command (check description [here](https://dev.bostondynamics.com/python/bosdyn-client/src/bosdyn/client/robot_command#bosdyn.client.robot_command.RobotCommandBuilder.synchro_se2_trajectory_point_command))

## Conclusion

Now you know how to:
- get photos from all the Spot's cameras
- list world objects around robot
- move between those objects

