
# Set a Config variable from the command line

## Not-automatic variables

You can set config variable option from the command line as well as from an INI file with the "-ini" command line option.


### Generic Formatting

```ini
-ini:<Config File>:[<category>]:<your config value>
```

"Config File" would be whatever config file you would normally set this on, such as the Engine, Game, Input, Editor, etc. Anything that has a "Default.ini" file.

### Command Line Specific Example

```ini
-ini:Engine:[OnlineSubsystem]:DefaultPlatformService=EOSPlus
```

Example: Set default platform service for the Online Subsystem, which would normally go in your DefaultEngine.ini file.

### Config File Equivalent

```ini
; In your DefaultEngine.ini file... 

[OnlineSubsystem]
DefaultPlatformService=EOSPlus
```

This is the equivalent of the command line option above as it would appear in the .ini file.

## Change config files from console



```ini
-customconfig=EOS
```

