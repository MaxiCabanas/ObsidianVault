- [FRunnable](#frunnable)
	- [What is FRunnable?](#what-is-frunnable)
	- [How to use FRunnable](#how-to-use-frunnable)
	- [Usage in Game Code](#usage-in-game-code)
	- [Best Practices](#best-practices)
	- [Summary](#summary)

## FRunnable

### What is FRunnable?

FRunnable is a base class in Unreal Engine that allows you to create and manage threads easily. It provides a simple interface for creating and controlling background threads.

Key points:
- Allows creating separate threads for CPU-intensive tasks
- Provides methods for initialization, running, stopping, and exiting the thread
- Handles thread creation and management internally

### How to use FRunnable

1. Create a subclass of FRunnable
2. Override required virtual methods (Init, Run, Stop)
3. Create an instance and start the thread

Code example:

```cpp
class FMyWorker : public FRunnable
{
public:
    FMyWorker();
    virtual ~FMyWorker();

    virtual bool Init() override;
    virtual uint32 Run() override;
    virtual void Stop() override;

private:
    FRunnableThread* Thread;
};

FMyWorker::FMyWorker()
{
    Thread = FRunnableThread::Create(this, TEXT("MyWorkerThread"));
}

FMyWorker::~FMyWorker()
{
    delete Thread;
}

bool FMyWorker::Init()
{
    return true;
}

uint32 FMyWorker::Run()
{
    while (/* some condition */)
    {
        // Perform work here
    }
    return 0;
}

void FMyWorker::Stop()
{
    // Cleanup
}
```

### Usage in Game Code

```cpp
FMyWorker* Worker = new FMyWorker();
// Worker runs automatically after construction

// To stop the thread later
Worker->Stop();
delete Worker;
```

### Best Practices

- Use for CPU-bound tasks only
- Avoid accessing game objects from the thread
- Use synchronization primitives carefully if needed
- Properly clean up resources in Stop()

### Summary

FRunnable simplifies thread creation and management in UE5. It handles low-level details, allowing you to focus on implementing your threaded logic. By following the pattern of overriding Init, Run, and Stop, you can easily offload computationally expensive tasks to background threads.

Citations:
[1] https://unrealcommunity.wiki/multithreading-with-frunnable-2a4xuf68
[2] https://benui.ca/unreal/frunnable-threads/
[3] https://store.algosyntax.com/tutorials/unreal-engine/ue5-multithreading-with-frunnable-and-thread-workflow/?srsltid=AfmBOoq0Gyr9t6-lQ7ZJ9knLGQ68XgFjnwexZHr4nO9XvpsoZjo-hZKy
[4] https://forums.unrealengine.com/t/could-i-get-some-help-with-a-frunnable-and-frunnablethread-problem/283580
[5] https://www.youtube.com/watch?v=UyloKYQpYFM
[6] https://forums.unrealengine.com/t/multithreading-and-performance-in-unreal/1216417
[7] https://inoland.net/unreal-engine-5-multithreading/
[8] https://www.youtube.com/watch?v=tGNaDagBq8E
[9] https://www.reddit.com/r/unrealengine/comments/4yt8f2/when_to_use_the_task_graph_system_when_to_use/
[10] https://www.reddit.com/r/unrealengine/comments/1c665dm/difference_and_usecases_for_task_graph_tasks/