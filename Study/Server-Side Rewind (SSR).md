Server-Side Rewind its a technique used in games to calculate the state of a game or elements in it at an arbitrary moment in the past, usually a few milliseconds back.

A practical application for this is lag compensation in shooting validation. In order for the server to actually validates if a client's shot was accurate we need to know the position, rotation and possibly other variables of the victim at the time the client actually took the shot.

So, the server checks the instigator's shoot data against the victim's information at the time the shot was taken (essentially the current time minus the instigator latency)

# Implementation overview

A simple implementation of this technique in UE5 would be an ActorComponent that saves all the relevant information in the server representation of the actors and whenever the information is needed we simply consult this history of data.

Sources:
- https://medium.com/@PanoVerse/implementation-of-server-side-rewind-in-unreal-engine-a-deep-dive-into-lag-compensation-ae565ec4af36
- https://vorixo.github.io/devtricks/simple-rewinding/