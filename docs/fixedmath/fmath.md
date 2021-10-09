## Description
A collection of common math functions.

| **Static Properties**  | **Description**  |  **Mathf**     |  **FMath**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| [Deg2Rad][1]       |Degrees-to-radians conversion constant (Read Only).| :material-check: |:material-check: |
| Epsilon       |A tiny floating point value (Read Only).| :material-check: |:material-check:[^1] |
| Infinity    |A representation of positive infinity (Read Only).| :material-check: |:material-close:[^2] |
| NegativeInfinity       |A representation of negative infinity (Read Only).| :material-check: |:material-close:[^3] |
| PI    |The well-known 3.14159265358979... value (Read Only).| :material-check: |:material-check: |
| Rad2Deg    |Radians-to-degrees conversion constant (Read Only).| :material-check: |:material-check: |



| **Static Methods**  | **Description**  |  **Mathf**     |  **FMath**   | 
| ----------- |----------- | ----------- |------------------------------------ |
| Abs	|Returns the absolute value of f.| :material-check: |:material-check: |
| Acos	|Returns the arc-cosine of f - the angle in radians whose cosine is f.| :material-check: |:material-check: |
| Approximately	|Compares two floating point values and returns true if they are similar.| :material-check: |:material-check: |
| Asin	|Returns the arc-sine of f - the angle in radians whose sine is f.| :material-check: |:material-check: |
| Atan	|Returns the arc-tangent of f - the angle in radians whose tangent is f.| :material-check: |:material-check: |
| Atan2	|Returns the angle in radians whose Tan is y/x.| :material-check: |:material-check: |
| Ceil	|Returns the smallest integer greater to or equal to f.| :material-check: |:material-check: |
| CeilToInt	|Returns the smallest integer greater to or equal to f.| :material-check: |:material-check: |
| Clamp	|Clamps the given value between the given minimum float and maximum float values. Returns the given value if it is within the min and max range.| :material-check: |:material-check: |
| Clamp01	|Clamps value between 0 and 1 and returns value.| :material-check: |:material-check: |
| ClosestPowerOfTwo	|Returns the closest power of two value.| :material-check: |:material-close: |
| CorrelatedColorTemperatureToRGB	|Convert a color temperature in Kelvin to RGB color.| :material-check: |:material-close: |
| Cos	|Returns the cosine of angle f.| :material-check: |:material-check: |
| DeltaAngle	|Calculates the shortest difference between two given angles given in degrees.| :material-check: |:material-check: |
| Exp	|Returns e raised to the specified power.| :material-check: |:material-check: |
| FloatToHalf	|Encode a floating point value into a 16-bit representation.| :material-check: |:material-check: |
| Floor	|Returns the largest integer smaller than or equal to f.| :material-check: |:material-check: |
| FloorToInt	|Returns the largest integer smaller to or equal to f.| :material-check: |:material-check: |
| GammaToLinearSpace	|Converts the given value from gamma (sRGB) to linear color space.| :material-check: |:material-close: |
| HalfToFloat	|Convert a half precision float to a 32-bit floating point value.| :material-check: |:material-check: |
| InverseLerp	|Calculates the linear parameter t that produces the interpolant value within the range [a, b].| :material-check: |:material-check: |
| IsPowerOfTwo	|Returns true if the value is power of two.| :material-check: |:material-close: |
| Lerp	|Linearly interpolates between a and b by t.| :material-check: |:material-check: |
| LerpAngle	|Same as Lerp but makes sure the values interpolate correctly when they wrap around 360 degrees.| :material-check: |:material-check: |
| LerpUnclamped	|Linearly interpolates between a and b by t with no limit to t.| :material-check: |:material-check: |
| LinearToGammaSpace	|Converts the given value from linear to gamma (sRGB) color space.| :material-check: |:material-close: |
| Log	|Returns the logarithm of a specified number in a specified base.| :material-check: |:material-check: |
| Log10	|Returns the base 10 logarithm of a specified number.| :material-check: |:material-check: |
| Max	|Returns largest of two or more values.| :material-check: |:material-check: |
| Min	|Returns the smallest of two or more values.| :material-check: |:material-check: |
| MoveTowards	|Moves a value current towards target.| :material-check: |:material-check: |
| MoveTowardsAngle	|Same as MoveTowards but makes sure the values interpolate correctly when they wrap around 360 degrees.| :material-check: |:material-check: |
| NextPowerOfTwo	|Returns the next power of two that is equal to, or greater than, the argument.| :material-check: |:material-close: |
| PerlinNoise	|Generate 2D Perlin noise.| :material-check: |:material-close: |
| PingPong	|PingPong returns a value that will increment and decrement between the value 0 and length.| :material-check: |:material-check: |
| Pow	|Returns f raised to power p.| :material-check: |:material-check: |
| Repeat	|Loops the value t, so that it is never larger than length and never smaller than 0.| :material-check: |:material-check: |
| Round	|Returns f rounded to the nearest integer.| :material-check: |:material-check: |
| RoundToInt	|Returns f rounded to the nearest integer.| :material-check: |:material-check: |
| Sign	|Returns the sign of f.| :material-check: |:material-check: |
| Sin	|Returns the sine of angle f.| :material-check: |:material-check: |
| SmoothDamp	|Gradually changes a value towards a desired goal over time.| :material-check: |:material-check: |
| SmoothDampAngle	|Gradually changes an angle given in degrees towards a desired goal angle over time.| :material-check: |:material-check: |
| SmoothStep	|Interpolates between min and max with smoothing at the limits.| :material-check: |:material-check: |
| Sqrt	|Returns square root of f.| :material-check: |:material-check: |
| Tan	|Returns the tangent of angle f in radians.| :material-check: |:material-check: |

[^1]: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
[^2]: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
[^3]: Lorem ipsum dolor sit amet, consectetur adipiscing elit.

[1]: reference/fmath-deg2rad.md