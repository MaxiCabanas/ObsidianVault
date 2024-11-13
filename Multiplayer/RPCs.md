From UE5 documentation:

> **RPCs** (**Remote Procedure Calls**) are functions that are called locally, but executed remotely on another machine (separate from the calling machine).
> 
> RPC functions can be very useful and allow either the client or the server to send messages to each other over a network connection.
> 
> The primary use case for these features are to do unreliable gameplay events that are transient or cosmetic in nature. These could include events that do things such as play sounds, spawn particles, or do other temporary effects that are not crucial to the Actor functioning. Previously these types of events would often be replicated via Actor properties.
> 
> When using RPCs, it it also important to understand [how ownership works](https://dev.epicgames.com/documentation/en-us/unreal-engine/actors-and-their-owning-connections?application_version=4.27), since it determines where most RPCs will run.

### RPC invoked from the server

| Actor ownership        | Not replicated | `NetMulticast`                 | `Server`       | `Client`                      |
| ---------------------- | -------------- | ------------------------------ | -------------- | ----------------------------- |
| **Client-owned actor** | Runs on server | Runs on server and all clients | Runs on server | Runs on actor's owning client |
| **Server-owned actor** | Runs on server | Runs on server and all clients | Runs on server | Runs on server                |
| **Unowned actor**      | Runs on server | Runs on server and all clients | Runs on server | Runs on server                |

### RPC invoked from a client

| Actor ownership                 | Not replicated          | `NetMulticast`          | `Server`       | `Client`                |
| ------------------------------- | ----------------------- | ----------------------- | -------------- | ----------------------- |
| **Owned by invoking client**    | Runs on invoking client | Runs on invoking client | Runs on server | Runs on invoking client |
| **Owned by a different client** | Runs on invoking client | Runs on invoking client | Dropped        | Runs on invoking client |
| **Server-owned actor**          | Runs on invoking client | Runs on invoking client | Dropped        | Runs on invoking client |
| **Unowned actor**               | Runs on invoking client | Runs on invoking client | Dropped        | Runs on invoking client |

## Validation

> Recently, the ability to add validation functions to RPCs was added to serve as a choke point for detecting bad data/inputs. The idea is if the validation function for an RPC detected that any of the parameters were bad, it could notify the system to disconnect the client/server who initiated the RPC call.

```c++
UFUNCTION(Server, WithValidation)
void SomeRPCFunction(int32 AddHealth);
```

```c++
bool SomeRPCFunction_Validate(int32 AddHealth)
{
	if (AddHealth > MAX_ADD_HEALTH)
	{
		return false; // This will disconnect the caller
	}
	return true; // This will allow the RPC to be called
}

void SomeRPCFunction_Implementation(int32 AddHealth)
{
	Health += AddHealth;
}
```

https://dev.epicgames.com/documentation/en-us/unreal-engine/rpcs?application_version=4.27

