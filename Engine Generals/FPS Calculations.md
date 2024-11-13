The engine stores the average FPS and MS of the last 10 frames as global engine variables

```cpp
// UnrealEngine.cpp
// We expose these variables to everyone as we need to access them in other files via an extern  
ENGINE_API float GAverageFPS = 0.0f;  
ENGINE_API float GAverageMS = 0.0f;  
ENGINE_API float GAveragePathTracedMRays = 0.0f;  
ENGINE_API double GLastMemoryWarningTime = 0.f;
```

This is how its calculated

```cpp
// UnrealEngine.h
// Calculate the average frame time by using the stats system.  
inline void CalculateFPSTimings()  
{  
    extern ENGINE_API float GAverageFPS;  
    extern ENGINE_API float GAverageMS;  
    // Calculate the average frame time via continued averaging.  
    static double LastTime = 0;  
    double CurrentTime    = FPlatformTime::Seconds();  
    float FrameTime          = (CurrentTime - LastTime) * 1000;  
    // A 3/4, 1/4 split gets close to a simple 10 frame moving average  
    GAverageMS          = GAverageMS * 0.75f + FrameTime * 0.25f;  
    LastTime            = CurrentTime;  
    // Calculate average framerate.  
    GAverageFPS = 1000.f / GAverageMS;  
}
```
