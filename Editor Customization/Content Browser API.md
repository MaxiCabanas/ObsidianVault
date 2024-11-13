
# Create assets in C++

```C++
// Determine an appropriate name  
FString Name;  
FString PackagePath;  
CreateUniqueAssetName(Object->GetOutermost()->GetName(), DefaultSuffix, PackagePath, Name);  
  
// Create the factory used to generate the asset  
USoundCueFactoryNew* Factory = NewObject<USoundCueFactoryNew>();  
Factory->InitialSoundWaves = Objects;  
  
FContentBrowserModule& ContentBrowserModule = FModuleManager::LoadModuleChecked<FContentBrowserModule>("ContentBrowser");  
ContentBrowserModule.Get().CreateNewAsset(Name, FPackageName::GetLongPackagePath(PackagePath), USoundCue::StaticClass(), Factory);
```
# Select Asset in content drawer

```c++
Info.Hyperlink = FSimpleDelegate::CreateLambda([SoftObjectPath] {  
    // Select the cloud in Content Browser when the hyperlink is clicked  
    TArray<FAssetData> AssetData;
    static FAssetRegistryModule& AssetRegistryModule = FModuleManager::LoadModuleChecked<FAssetRegistryModule>("AssetRegistry");
    const FAssetData& AssetData = AssetRegistryModule.Get().GetAssetByObjectPath(SoftObjectPath.GetWithoutSubPath());
    AssetData.Add(AssetData);
    FModuleManager::LoadModuleChecked<FContentBrowserModule>("ContentBrowser").Get().SyncBrowserToAssets(AssetData);  
    });
```

# Open Select Directory windows

```c++
if (ExportPath.IsEmpty())  
{  
    // If not prompting individual files, prompt the user to select a target directory.  
    IDesktopPlatform* DesktopPlatform = FDesktopPlatformModule::Get();  
	
	if (DesktopPlatform)  
    {
		FString FolderName;  
		const FString Title = NSLOCTEXT("UnrealEd", "ChooseADirectory", "Choose A Directory").ToString();  
		const bool bFolderSelected = DesktopPlatform->OpenDirectoryDialog(
	       FSlateApplication::Get().FindBestParentWindowHandleForDialogs(nullptr),
	       Title,
	       LastExportPath,
	       FolderName);  
	       
		if (bFolderSelected)
	    {
	       SelectedExportPath = FolderName;
		}
	}
}
```

#Editor #Links #ContentDrawer 