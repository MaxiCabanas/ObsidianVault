
```c++
TSharedRef<FNotificationInfo> UBSCommonEditorFunctionLibrary::CreateNotificationInfo(const FString& Content)  
{  
    const FString InfoContent = FString::Format(TEXT("Burro ERROR: {0}"), {Content});  
    FNotificationInfo* TempInfo = new FNotificationInfo(FText::FromString(InfoContent));  
       TempInfo->bUseLargeFont = true;  
    TempInfo->ExpireDuration = 5.0f;  
    TempInfo->WidthOverride = 500.0f;  
    TempInfo->bUseSuccessFailIcons = true;  
    TSharedRef<FNotificationInfo> Info = MakeShareable<FNotificationInfo>(TempInfo);  
    // FNotificationInfo Info(FText::FromString(InfoContent));  
    return Info;  
}
```

#Editor #CustomNotification