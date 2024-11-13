
## ____FUNCTION____  predefined macro

In UE5 this C++ predefined macro can be used to get the name of the current **function** from which is being used, including **namespace** and **class name**

```c++
#define LOG_FUNCTION_NAME() UE_LOG(TempLog, Display, TEXT("%s"), ANSI_TO_CHAR(__FUNCTION__));

UCLASS()
class MY_GAME_API AMyActor : public AActor
{
public:
	void PrintName()
	{
		LOG_FUNCTION_NAME(); // This will print MY_GAME_API::AMyActor::PrintName()
	}
}
```

Rama examples:
https://nerivec.github.io/old-ue4-wiki/pages/logs-printing-class-name-function-name-line-number-of-your-calling-code.html