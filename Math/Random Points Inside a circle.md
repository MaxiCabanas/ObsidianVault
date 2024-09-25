There are a few approaches to generate points uniformly distributed inside a  circle

# Rejection Sampling

This method is one of the simplest and very performant too.

We pick a random coordinate inside a square using the cartesian system, then we test if the point is inside the circle, if not we simply pick another.

![](Media/Pasted%20image%2020240925150922.png)


```c++
const float SquareSize = 100;
const float R = 50;

// Generation of the point is trivial
FVector2D GenerateRandomPointInSquare()
{
	const float X = FMath::RandRange(0, SquareSize);
	const float Y = FMath::RandRange(0, SquareSize);
	return FVector2D(X, Y);
}

// General solution
bool IsInCircle(const FVector& Point)
{
	// Distance = Sqrt((v2.x - v1.x)^2 + (v2.y - v1.y)^2)
	return Point.Distance(CircleCenter) < R;
}

// Faster version, avoiding the slow sqrt function.
bool IsInCircleSquared(const FVector& Point)
{
	// DistSquared = (v2.x - v1.x)^2 + (v2.y - v1.y)^2
	return Point.DistSquared(Point) < R*R;
}

// Even faster version, testing every case individually and avoiding math when possible.
bool IsInCircleFast(const FVector& Point)
{
	float DistX = FMath::Abs(Point.x - CircleCenter.x);
	if (DistX > R)
		return false;
		
	float DistY = FMath::Abs(Point.y - CircleCenter.y);
	if (DistY > R)
		return false;
		
	if (DistX + DistY <= R)
		return true;
		
	return (DistX*DistX + DistY*DistY <= R*R);
}
```

*"IsInCircleFast" performance was measured by a user here:*
https://stackoverflow.com/questions/481144/equation-for-testing-if-a-point-is-inside-a-circle

The probability of a point to be inside of the circle is the "Area of circle" divided by "Area of square", so, for a radius = 1 we can know:

$$
\text{Success Rate: }\frac{\pi*1{^2}}{2*2} = \frac{\pi}{4} \approx 0.785 
$$

$$
\text{Fail n Times: }\left( 1-\frac{\pi}{4} \right){^n}
$$

![](Media/Pasted%20image%2020240925145716.png)

We can calculate the average number of attempt to get a valid point as:

$$
\text{Expected n = } \frac{1}{\frac{\pi}{4}} = \frac{4}{\pi} \approx 1.273
$$
This means that for every 100 valid dots we obtain we must sample an average of ~127 dots

in [this p5 example](https://editor.p5js.org/MaxiCabanas/sketches/aLU1HUoDa) we can see that this is true

https://stackoverflow.com/questions/5837572/generate-a-random-point-within-a-circle-uniformly
https://en.wikipedia.org/wiki/Cumulative_distribution_function
https://en.wikipedia.org/wiki/Polar_coordinate_system
https://www.youtube.com/watch?v=4y_nmpv-9lI


