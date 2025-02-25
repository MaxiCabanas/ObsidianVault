Let's say we have to gather data from all instances of every relevant class in our game at certain point, for instance, at the end of the level, and show all that information as a summary or tally screen.

We are talking about a lot of unrelated classes, enemies, interactable objects, the player, environment objects, etc.

We could just implement a function in every class that send that data to a manager or whatever at the specific time we need it, but if we need to change something about the behavior of the feature, like the time at what the data is sent, we could need to change that in every class. Also the implementation of that function will seem totally unrelated and alien in those classes.

One possible solution is to implement those functions inside the manager itself, but because every class is totally different from the others we gonna need a function per class

```c++
...
if (Object.Is(EnemyClass))
{
GatherEnemyData(Object);
} 
else if (Object.Is(InteractableClass))
{
GatherInteractableData();
} 
else if...
```

That means our manager would need to cast the object and call the specific function for the correct class. This could or could not be a problem, but if we are gathering data for a lot of instances, we surely don't want to do this.

Visitor Pattern eliminates this problem leaving the choice of the specific function to the object itself.

Every object that can be asked for data implements an interface, lets call it *VisitableInterface*, with a pure method void AcceptVisit(Visitor). Now our manager calls this method and passes itself as a visitor.

```c++
...
// inside our manager:
for (i=0; i<AllObjects; i++)
{
	VisitableInterface* Object = AllObjects[i];
	Object.AcceptVisit(this);
}
...
```

and because every object knows its own class they can simply call the correct function:

```c++
// Enemy class
void Enemy::AcceptVisit(OurManager* Visitor)
{
	Visitor.GatherEnemyData(this);
}
// Interactable class
void Interactable::AcceptVisit(OurManager* Visitor)
{
	Visitor.GatherInteractableData(this);
}
// Player class
void Player::AcceptVisit(OurManager* Visitor)
{
	Visitor.GatherPlayerData(this);
}
```

More info in sources

sources:
- https://refactoring.guru/design-patterns/visitor