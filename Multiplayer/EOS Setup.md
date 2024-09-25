# Fix PersistantAuth in CommonUser:

```c++
bool UCommonUserSubsystem::AutoLoginOSSv1(FOnlineContextCache* System, TSharedRef<FUserLoginRequest> Request, FPlatformUserId PlatformUser)  
{  
    return System->IdentityInterface->AutoLogin(GetPlatformUserIndexForId(PlatformUser));  
}
```