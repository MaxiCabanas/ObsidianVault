There is a way to link an Asset to a MarkdownAsset. 

For now:

```c++
UProperty(EditDefaultsOnly)
TMap<TSoftPtr<UMarkdownAsset>,TSoftPtr<UObject>> MarkdownFilesPerAsset
```
