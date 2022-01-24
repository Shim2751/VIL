# Carla_Sensor(Ros Bridge)

document: https://carla.readthedocs.io/projects/ros-bridge/en/latest/carla_spawn_objects/#spawning-sensors

ros-bridge repository: https://github.com/carla-simulator/ros-bridge/blob/master/carla_spawn_objects/config/objects.json

blueprint library: https://carla.readthedocs.io/en/latest/bp_library/

## 기본 명령어

```
roslaunch carla_spawn_objects carla_spawn_objects.launch
```

## sensor 추가
1. blueprint library에서 원하는 sensor와 attribute를 확인한다.
2. ```~/carla-ros-bridge/catkin_ws/src/ros-bridge/carla_spawn_objects/config/objects.json```에 json 형식에 맞추어 추가를 해주면 된다.

```
{
        "type": "<SENSOR-TYPE>",
        "id": "<NAME>",
        "spawn_point": {"x": 0.0, "y": 0.0, "z": 0.0, "roll": 0.0, "pitch": 0.0, "yaw": 0.0},
        <ADDITIONAL-SENSOR-ATTRIBUTES>
        }
```
