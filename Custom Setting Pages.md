

# UDeveloperSettings

Creating a custom DeveloperSettings is a great way to expose the settings for a feature of our game to a place where can be tweak convenient and that makes sense. 
Because settings are saved in a .ini file, can be tweaked for a built game, which makes this approach extremely flexible.
On top of those benefits, those settings can be used to set a [[ConsoleVariable]] value which makes the settings be tweakable from [[editor console]] in runtime.

To create a custom DeveloperSettings section in [[ProjectSettings]] we need to create a new class that inherits from UDeveloperSettings (or UDeveloperSettingsBackedByCVars if we want to support ConsoleVariables)

```c++
UCLASS(Config=PlayerSettings, DefaultConfig)  
class GAME_API UPlayerSettings : public UDeveloperSettingsBackedByCVars  
{  
    GENERATED_BODY()  
  
public:  
      
    /** Default FOV in Degrees. */  
    UPROPERTY(Config, EditDefaultOnly, Category="Camera", meta=(ConsoleVariable="mygame.Player.DefaultFOV")  
    float DefaultFOV = 90.0f;
      
protected:
	
	virtual FName GetCategoryName() const override { return FName(TEXT("MyGame")); }  
      
    virtual FName GetSectionName() const override { return FName(TEXT("Player Settings")); }
}
```

Overriding GetCategoryName() and GetSectionName() we control how the settings will be shown in [[ProjectSettings]].

# UEditorSettings
-

# Open CustomSettings in editor from C++

Usually when working with customs subclasses of [UDeveloperSettings](Custom%20Setting%20Pages.md#UDeveloperSettings) we want to enforce setting up some variables or references.

A way to do this is using the [[ConsoleOutput]] or a custom [[Editor Notification]]. Both solutions, as many others, support the inclution of Hyperlinks that the user can click to navigate directly to any point in the editor, we can use this feature to expose a link to our custom [[Custom Setting Pages#UDeveloperSettings|UDeveloperSettings]]

Let's say we have a custom UDeveloperSettings:

```c++
UCLASS(Config=CustomConfigFile, DefaultConfig)  
class UCustomDeveloperSettings : public UDeveloperSettings
{  
    GENERATED_BODY()  
    
};
```

You can open the settings page in the editor with the following code:

```c++
const UCustomDeveloperSettings* Settings = GetDefault<UCustomDeveloperSettings>();
static ISettingsModule& SettingsModule = FModuleManager::LoadModuleChecked<ISettingsModule>("Settings");

const FName& ContainerName = Settings.GetContainerName();
const FName& CategoryName = Settings.GetCategoryName();
const FName& SectionName = Settings.GetSectionName();

SettingsModule.ShowViewer(ContainerName, CategoryName, SectionName);
```

A good idea is to wrap that behavior in two helper functions, so its easier to do from anywhere. 
As example see the next codeblock is extracted from the UStormSyncTransportSettings class from the engine code.

```c++
const UStormSyncTransportSettings& UStormSyncTransportSettings::Get()  
{  
    const UStormSyncTransportSettings* Settings = GetDefault<UStormSyncTransportSettings>();  
    check(Settings);  
    return *Settings;  
}  

#if WITH_EDITOR  
void UStormSyncTransportSettings::OpenEditorSettingsWindow() const  
{  
    static ISettingsModule& SettingsModule = FModuleManager::LoadModuleChecked<ISettingsModule>("Settings");
    SettingsModule.ShowViewer(GetContainerName(), GetCategoryName(), SectionName);
}  
#endif //WITH_EDITOR
```

Now we can open the setting page with just one line
```c++
UStormSyncTransportSettings::Get().OpenEditorSettingsWindow();
```


#Links #Editor #DeveloperSettings #EditorSettings #CustomSettings