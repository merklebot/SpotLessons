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
```
1. Register `WorldObjectClient`
2. Check the list of available world objects with `list_world_objects`. To filter only fiducials, use `object_type` param:
```python
response = world_object_client.list_world_objects(object_type=[world_object_pb2.WORLD_OBJECT_APRILTAG])
```
3. Get list of (filtered) objects as `world_object` field of response. And choose required fiducial:
```python
fiducial = response.world_objects[0]
```
4. Prepare coordinate transformation from AprilTag frame to some world (e.g. VISION_FRAME) coords, and get them to


## Conclusion

Now you know how to:
- get photos from all the Spot's cameras
- list world objects around robot
- move between those objects

