# VIL_Sensor

##UE를 위한 cpp class 생성법

###기본 틀

```
UCLASS()                                                          ///엔진이 클래스를 인식할 수 있도록 한다.
class [PROJECTNAME]_API ASafeDistanceSensor: public ASensor       ///부모 클래스를 Sensor로 설정
{
GENERATED_BODY() 

public:

private:
};
```
https://docs.unrealengine.com/4.27/ko/ProgrammingAndScripting/ClassCreation/CodeOnly/
