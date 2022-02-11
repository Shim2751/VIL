# Import a vehicle in Carla

## 1. Bind the bone
* blender를 사용했습니다. 기본 이동 키:(1)회전: 마우스 휠, (2)이동: shift+휠

bone: 바퀴가 좌 우로 움직일 수 있게 해주는 것이라 생각하면 된다.
mesh: 그물망 형태의 도형. 여기선 자동차를 이루는 부품들이라 생각하면 된다.

1. 차량을 이루는 mesh가 매우 많은데 바퀴 4개와 몸체 1개로 만든다.

 shift+L_clike으로 여러 개를 선택해서 아래와 같이 join을 한다.
 Wheel에서도 같은 작업을 해준다.
 ![join](https://user-images.githubusercontent.com/67774946/153583812-cce0b956-30d3-4195-9482-0c76c33f7332.png)
 
2. 차량이 +x방향을 바라보고 xy평면 위에 있게 만들어준다.
 (1) G+X+(마우스로 조정)으로 높이를 맞춘다.
 (2) 왼쪽 출바에서 Rotation 클릭->Z축으로 돌리는 것 선택->-90입력
 ![x_forward](https://user-images.githubusercontent.com/67774946/153583829-12e38bfd-5d1f-43a3-864e-68fa75dbc939.png)
 
3. 툴을 이용해 Rigging한다.
Rigging: bone과 mesh를 연결해주는 작업

설치법과 적용법은 아래 사이트에서 How to install, How to use it을 읽어줍니다.
https://continuebreak.com/creations/ue4-vehicle-rigging-addon-blender/
사용법(1분 30초까지)
https://www.youtube.com/watch?v=laAs3lefrKY&t=24s
(1) 아래 5개는 삭제
![4](https://user-images.githubusercontent.com/67774946/153583846-370522a0-24dd-4729-8cb1-f764faedd5f9.png)

(2) Wheel과 Body의 이름을 위치에 맞게 아래와 같이 바꿔준다(안하면 오류남-blueprint할 때 이름 설정이 달라지기 때문에).
 Wheel_Front_Left, Wheel_Front_Right, Wheel_Rear_Left, Wheel_Rear_Right, VehicleBase
![5](https://user-images.githubusercontent.com/67774946/153583855-43963c19-87ca-4d50-a314-91eb3b91b8ae.png)

4. 바퀴 길이 측정
왼쪽 툴바에서 measure을 누르고 바퀴 반지름과 폭을 잰다(나중에 씀).
폭 21cm 반지름 67cm
![6](https://user-images.githubusercontent.com/67774946/153583868-0c248fb5-5959-4e1b-b771-02cb2aa1c37c.png)
![7](https://user-images.githubusercontent.com/67774946/153583873-c1600615-5af0-4734-bb93-0a703c800dba.png)

5. Export
(1) file->Export->fbx
(2) Setting을 다음과 같이 한다.
![8](https://user-images.githubusercontent.com/67774946/153584066-2bfa8a85-9246-46ca-95c6-223ceb7f9fe8.png)

## 2. Import and configure the vehicle
