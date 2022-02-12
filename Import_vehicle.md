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

(2) Wheel과 Body의 이름을 위치에 맞게 아래와 같이 바꿔준다(안하면 오류남-blueprint할 때 이름 설정이 달라지기 때문에).
 Wheel_Front_Left, Wheel_Front_Right, Wheel_Rear_Left, Wheel_Rear_Right, VehicleBase
![5](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/rigging.png)

### 4. 바퀴 길이 측정
왼쪽 툴바에서 measure을 누르고 바퀴 반지름과 폭을 잰다(나중에 씀).

폭 21cm 반지름 67cm
![6](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/calibration_1.png)
![7](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/calibration.png)

### 5. Export
(1) file->Export->fbx

(2) Setting을 다음과 같이 한다. 이름은 SM_Ioniq.fbx

![8](https://github.com/Shim2751/VIL_Sensor.github.io/blob/main/img/setting.png)

## 2. Import and configure the vehicle
### 1.Create the vehicle folder
Create a new folder named Ioniq in Content/Carla/Static/Vehicles/4Wheeled.
### 2.Import fbx file
Add/Import -> Import new asset
설정은 다음과 같다.
* Import Content Type: Geometry and Skinning Weights.
* Normal Import Method: Import Normals.
* Material Import Method: Do not create materials. 
* Uncheck Import Textures
### 3. Set the physical asset mesh.
1. SM_Ioniq_PhysicsAssets을 연다.
2.
3.
4. Save하고 종료
5. skelton에 들어가서 save하고 종료

### 4.Create the Animation Blueprint.

### 5.Configure the Animation Blueprint.

1. 다른 차의 Animation을 실행-> 드래그+ctrl+V해서 복사해온다.
2. Componet To Local과 Output Pose연결
3. Compile & Save

### 6. Prepare the vehicle and wheel blueprints.

### 7. Configure the wheel blueprints.
* collision Mesh: Wheel_shape
* Shape Radius: 67 
* Shape Width: 21
* Tire Config: CommonTireConfig
* (FW) Uncheck Affeted by Handlebrake (RW) Check Affeted by Handlebrake
* (FW) Steer Angle: 70 (RW) Steer Angle: 0 
Compile & Save
### 8. Configure vehicle blueprint.
### 9. Add the vehicle to the Blueprint Library.
