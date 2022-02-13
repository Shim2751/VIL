# Import a vehicle in Carla

## 1. Bind the bone
* blender를 사용했습니다. 기본 이동 키:(1)회전: 마우스 휠, (2)이동: shift+휠

bone: 바퀴가 좌 우로 움직일 수 있게 해주는 것이라 생각하면 된다.

mesh: 그물망 형태의 도형. 여기선 자동차를 이루는 부품들이라 생각하면 된다.

### 1. 차량을 이루는 mesh가 매우 많은데 바퀴 4개와 몸체 1개로 만든다.

 shift+L_clike으로 여러 개를 선택해서 아래와 같이 join을 한다.
 Wheel에서도 같은 작업을 해준다.
 ![1](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/join.png)
 
### 2. 차량이 +x방향을 바라보고 xy평면 위에 있게 만들어준다.
 (1) 왼쪽 출바에서 Rotation 클릭->Z축으로 돌리는 것 선택->-90입력
 (2) g+z+(마우스로 조정)으로 높이를 맞춘다.
 ![2](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/x_forward.png)
 
### 3. 툴을 이용해 Rigging한다.
Rigging: bone과 mesh를 연결해주는 작업

설치법과 적용법은 아래 사이트에서 How to install, How to use it을 읽어줍니다.
https://continuebreak.com/creations/ue4-vehicle-rigging-addon-blender/

사용법(1분 30초까지)
https://www.youtube.com/watch?v=laAs3lefrKY&t=24s

(1) 아래 5개는 삭제

![4](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/del.png)

![5](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/rigging.png)

### 4. 바퀴 길이 측정
왼쪽 툴바에서 measure을 누르고 바퀴 반지름과 폭을 잰다(나중에 씀).

폭 21cm 반지름 33.5cm
![6](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/calibration_1.png)
![7](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/calibration.png)

### 5. Export
(1) file->Export->fbx

(2) Setting을 다음과 같이 한다. 이름은 SM_Ioniq.fbx

![8](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/setting.png)

## 2. Import and configure the vehicle
### 1.Create the vehicle folder

Create a new folder named HundaiIoniq in Content/Carla/Static/Vehicles/4Wheeled.

### 2.Import fbx file

Add/Import -> Import new asset
설정은 다음과 같다.
* Import Content Type: Geometry and Skinning Weights.
* Normal Import Method: Import Normals.
* Material Import Method: create materials. 
* check Import Textures

### 3. Set the physical asset mesh.

1. SM_Ioniq_PhysicsAssets을 연다.

2. Root클릭하고 ```Primitive Type: Multi Convex Hull``` -> Re-generate Bodies

![9](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/Physics_body.png)

3. shift로 바퀴 4개 선택하고 ```Primitive Type: Sphere```,```Physics Type: Kinematic```, ```Linear Damping: 0.0``` -> Re-generate Bodies

![10](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/Physics_wheel.png)

4. Root와 바퀴 모두 선택하고 Simulation Generate를 check

![11](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/Physics_sim.png) 

5. Save

8. Mesh, Skelton에 들어가서 save하고 종료

### 4.Create the Animation Blueprint.

1.아래와 같이 Animation Blueprint를 만든다.

![12](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/create_AniBlue.png)

2. ```Parent Class: VehicleAnimInstance```,```Target Skeleton: SM_Ioniq_Skeleton```

![13](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/Screenshot%20from%202022-02-12%2022-08-37.png)

### 5.Configure the Animation Blueprint.

1. 다른 차의 Animation을 실행-> Output Pose 제외하고 드래그+ctrl+V해서 복사해온다.

2. Componet To Local과 Output Pose연결

3. Compile & Save
![14](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/Animation.png)

### 6. Prepare the vehicle and wheel blueprints.
0. Content/Carla/Blueprints/Vehicles에 HundaiIoniq 폴더를 만들어준다.

1. Blueprint를 만든다.

![15](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/create_blueprint.png)

2. 아래 같이 설정해서 Wheel Blueprint를 2개 만든다. 이름은 ```BP_Ioniq_FW```, ```BP_Ioniq_RW```

![16](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/blueprint_wheel.png)

3. 아래 같이 설정해서 Pawn Blueprint를 1개 만든다. 이름은 ```BP_Ioniq```

![17](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/blueprint_pawn.png)

### 7. Configure the wheel blueprints.
1. BP_Ioniq_FW와 BP_Ioniq_RW에 들어가서 다음과 같이 설정한다.

* collision Mesh: Wheel_shape
* Shape Radius: 33.5 
* Shape Width: 21
* Tire Config: CommonTireConfig
* (FW) Uncheck Affeted by Handlebrake (RW) Check Affeted by Handlebrake
* (FW) Steer Angle: 70 (RW) Steer Angle: 0

(FW를 setting한 사진)
![18](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/wheel_setting.png)
#### !주의 사진에서 Radius 입력을 잘못했다.

2. Compile & Save
### 8. Configure vehicle blueprint.

1. BP_Ioniq에 들어가 다음과 같이 설정한다.
* AnimClass: AniBP_Ioniq
* SkeletonMesh: SM_Ioniq
* WheelClass를 앞바퀴는 FW 뒷바퀴는 RW로 해준다.
* Bone name을 바꿔준다.

![19](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/pawn_setting1.png)
![20](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/pawn_setting.png)

### 9. Add the vehicle to the Blueprint Library.

1. Content/Carla/Blueprints/Vehicle에 있는 ```VehicleFactory```를 열어준다.

2. Vehicle을 클릭해 ```Make: Hundai```, ```Model: Ioniq```, ```Class: BP_Ioniq```으로 설정

### 10. Test

1. Launch CARLA, open a terminal in PythonAPI/examples and run the following command:

```python manual_control.py --filter <model_name>```
![21](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/final.png)

### 11.(Optional)Materials
1. 차량의 색을 유지하고 싶다면 Content/Carla/Static/Vehicles/4Wheeled/HundaiIoniq에 있는 Material들을 하나하나 열어서 저장하면 된다.
(안하면 다음에 Carla 실행시 지워져 있음)

![22] (https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/Materials.png)

###참고 사이트
https://carla.readthedocs.io/en/latest/tuto_A_add_vehicle/
https://continuebreak.com/creations/ue4-vehicle-rigging-addon-blender/
https://github.com/carla-simulator/carla/issues/2925
https://www.youtube.com/watch?v=0F3ugwkISGk
