# Static Delegates

Sometimes we need to implement interaction between classes from different layers. For example, let's take a look at Player class and it's interaction with some UI Widget. Let it be UI Widget for Game Menu with floating Show/Hide mechanic. The main thing - how can we pass some signal from Player to UI Widget. One approach - to include all stuff, use UGameplayStatics to get Player instance and so on. However, this approach make it a little bit too coupled.

```c++
#pragma once

#include "Delegates/DelegateCombinations.h"

class AMyDefaultPawn;

namespace UIDelegates {

	DECLARE_MULTICAST_DELEGATE_OneParam(FToggleMenuEvent, AMyDefaultPawn*);

	extern FToggleMenuEvent OnToggleMenu;
};
```
