# VIL_Sensor

Guide : https://carla.readthedocs.io/en/latest/core_sensors/

Sensor reference : https://carla.readthedocs.io/en/latest/ref_sensors/

##Setting

1. reference에서 사용하고자 하는 sensor의 blueprint와 attribute를 확인한다.
2. 아래 코드와 같이 setting한다. (bluprint는 센서 종류, attribute는 센서의 설정값)
```
# Find the blueprint of the sensor.
blueprint = world.get_blueprint_library().find('sensor.camera.rgb')

# Modify the attributes of the blueprint to set image resolution and field of view.
blueprint.set_attribute('image_size_x', '1920')
blueprint.set_attribute('image_size_y', '1080')
blueprint.set_attribute('fov', '110')

# Set the time in seconds between sensor captures
blueprint.set_attribute('sensor_tick', '1.0')
```

##Spawning
https://carla.readthedocs.io/en/latest/python_api/#commandspawnactor

1. world.spawn_actor 명령어를 사용하여 sensor를 불러낸다.
2. sensor의 위치는 ```attach_to = ```(주로 vehicle)과의 상대적 위치이고 transform으로 설정해주면 된다. 
```
transform = carla.Transform(carla.Location(x=0.8, z=1.7))
sensor = world.spawn_actor(blueprint, transform, attach_to=my_vehicle)
```

*sensor의 위치 설정을 Rigid attachment와 SpringArm attachment가 있다.

##Listening

1. ```listen()``` method를 통해 sensor의 데이터를 가져올 수 있다.
https://carla.readthedocs.io/en/latest/python_api/#carla.Sensor.listen
