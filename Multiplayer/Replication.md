![](Media/Pasted%20image%2020241003195352.png)
## Debug Networking

```c++
// Console commads:
// Make server reconciles visible
p.netshowcorrections 1

// Set the lifetime for the debug capsules of p.netshowcorrections
p.NetCorrectionLifetime 5
```

```c++
// Use the following commands to emulate lag
#define BUILD_NETEMULATION_CONSOLE_COMMAND(CommandName, CommandHelp) FAutoConsoleCommandWithWorldAndArgs NetEmulation##CommandName(TEXT("NetEmulation."#CommandName), TEXT(CommandHelp), \  
    FConsoleCommandWithWorldAndArgsDelegate::CreateStatic([](const TArray<FString>& Args, UWorld* World) \  
    { \  
       if (Args.Num() > 0) \  
       { \  
          CreatePersistentSimulationSettings(); \  
          FString CmdParams = FString::Printf(TEXT(#CommandName"=%s"), *(Args[0])); \  
          PersistentPacketSimulationSettings.GetValue().ParseSettings(*CmdParams, nullptr); \  
          ApplySimulationSettingsOnNetDrivers(World, PersistentPacketSimulationSettings.GetValue()); \  
       } \  
    }));  
  
    BUILD_NETEMULATION_CONSOLE_COMMAND(PktLoss, "Simulates network packet loss");  
    BUILD_NETEMULATION_CONSOLE_COMMAND(PktOrder, "Simulates network packets received out of order");  
    BUILD_NETEMULATION_CONSOLE_COMMAND(PktDup, "Simulates sending/receiving duplicate network packets");  
    BUILD_NETEMULATION_CONSOLE_COMMAND(PktLag, "Simulates network packet lag");  
    BUILD_NETEMULATION_CONSOLE_COMMAND(PktLagVariance, "Simulates variable network packet lag");  
    BUILD_NETEMULATION_CONSOLE_COMMAND(PktLagMin, "Sets minimum outgoing packet latency");  
    BUILD_NETEMULATION_CONSOLE_COMMAND(PktLagMax, "Sets maximum outgoing packet latency)");  
    BUILD_NETEMULATION_CONSOLE_COMMAND(PktIncomingLagMin, "Sets minimum incoming packet latency");  
    BUILD_NETEMULATION_CONSOLE_COMMAND(PktIncomingLagMax, "Sets maximum incoming packet latency");  
    BUILD_NETEMULATION_CONSOLE_COMMAND(PktIncomingLoss, "Simulates incoming packet loss");  
    BUILD_NETEMULATION_CONSOLE_COMMAND(PktJitter, "Simulates outgoing packet jitter");
```

You can also set preconfigured profiles using the autocomplete console function *NetEmulationPktEmulationProfile*
Check NetEmulationHelper.h for more context.


