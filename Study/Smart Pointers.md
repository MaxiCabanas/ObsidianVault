Smart pointers are objects that wraps a raw pointer and handles for us the management of memory, so instead of allocate or free memory manually when creating a pointer, a smart pointer will allocate the memory for us if needed and free the memory when the pointer is not needed anymore.
# Unique Pointer

Unique pointers solely and explicitly owns the object it references, this means that when the unique pointer falls out of scope the pointer inside is destroyed and the memory is freed. 

Also, a Unique Pointer cannot be copied.

```c++ error:5
void MyClass::MyFunction()
{
	{
		TUniquePtr<FMyStruct> MyUniquePtr = MakeUnique<FMyStruct>();
		TUniquePtr<FMyStruct> CopyUniquePtr = MyUniquePtr;
	}
}
```

In the example above, *"MyUniquePtr"* will only be usable inside the inner scope created in the line 3, so after line 6 the object will not exist anymore.

As the pointer cannot be copied, line 5 throws an error at compile time, since the Copy operator doesn't exists.

# Shared Pointer

Shared Pointers stores a blocks of memory that keeps tracks of the amount of strong references to the object inside. 

When the pointer is copied or a new reference is created the counter goes up, and when a Shared Pointer is destroyed the counter goes down. Once the reference counter reach zero the object is destroyed and memory is freed.

```c++ unwrap
void MyClass::MyFunction()
{
	TSharedPtr<FMyStruct> PtrOne;
	{
		TSharedPtr<FMyStruct> PtrTwo = MakeShared<FMyStruct>();
		PtrOne = PtrTwo; // Here the pointer is copied to PtrOne and the reference counter value is increased to 2.
	} // Here PtrTwo is destroyed and the reference counter value is decreased to 1
} // PtrOne is destroyed, reference counter is decreased to 0 and the object is automatically destroyed, 
```


> [!warning]
>There is a common problem that can occurs when using Shared Pointers called "Circular Link". 
>
>That is when two or more objects possess a reference to each other, keeping all instances alive for ever causing a memory leak.
>
>[Weak Pointers](Study/Smart%20Pointers.md#Weak%20Pointer) offer a solution to this and other scenarios.

# Weak Pointer

Weak Pointer works very similar to Shared Pointers but with the difference that it doesn't owns the object inside of it, so it doesn't increase the reference counter.

Because a object referenced by a Weak Pointer might not even exist anymore you first have to check if the referenced object is still alive.

```c++ unwrap
void MyClass::MyFunction()
{
	TWeakPtr<FMyStruct> MyWeakPtr;
	{
		TSharedPtr<FMyStruct> MySharedPtr = MakeShared<FMyStruct>();
		MyWeakPtr = MySharedPtr; // Here the pointer is copied to MyWeakPtr, the reference counter keeps its value.
		if (MyWeakPtr.IsValid()) // This is true here
		{
			...
		}
	}
	
	if (MyWeakPtr.IsValid()) // This is false here, as MySharedPtr fell out of scope, destroying the object inside it as no other reference existed.
	{
		...
	}
}
```

> [!info] Usage cases
> This type of pointer it's pretty useful when working with objects that might not exists and, maybe more important, that you don't want to keep alive.
> 
> You don't want that your flame thrower to keeps whatever is attacking's class instance alive in memory, since it can be an enemy that already has been killed.
> 
> Using Weak Pointes to dealing with this problem you can be sure that only if the enemy instance is still alive you will be able to work with it and make damage, and once the enemy HP is 0 your weapon will not keep alive the instance.

