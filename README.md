# Towel

<img src="./Logo.svg" height="150">

"It's a tough galaxy. If you want to survive, you've gotta know... where your towel is." - Ford Prefect

Towel is a C# .Net Standard libary intended to add much needed functionality that is missing in C# as well as redesign some aspects to bring the language up to modern standards.

Source Code: https://github.com/ZacharyPatten/Towel

Build [![Build Status](https://dev.azure.com/ZacharyPatten/Towel/_apis/build/status/ZacharyPatten.Towel?branchName=master)](https://dev.azure.com/ZacharyPatten/Towel/_build/latest?definitionId=1&branchName=master)

*Many features are coded and working, but Towel is still in heavy development. It should be ready for its first release later this year.*

## Mathematics

Towel has fast generic mathematics functions.

### Fundamental Operations
```csharp
T Add<T>(T a, T b);
T Negate<T>(T a);
T Subtract<T>(T a, T b);
T Multiply<T>(T a, T b);
T Divide<T>(T a, T b);
T Modulo<T>(T a, T b);
```
### More Numeric Mathematics
```csharp
void FactorPrimes<T>(T a, Step<T> step);
T Factorial<T>(T a);
T LinearInterpolation<T>(T x, T x0, T x1, T y0, T y1);
T LeastCommonMultiple<T>(T a, T b, params T[] c);
T GreatestCommonFactor<T>(T a, T b, params T[] c);
LinearRegression2D<T>(Stepper<T, T> points, out T slope, out T y_intercept);
```
### Statistics
```csharp
T Mean<T>(T a, params T[] b);
T Median<T>(params T[] values);
Heap<Link<T, int>> Mode<T>(T a, params T[] b);
void Range<T>(out T minimum, out T maximum, Stepper<T> stepper);
T[] Quantiles<T>(int quantiles, Stepper<T> stepper);
T GeometricMean<T>(Stepper<T> stepper);
T Variance<T>(Stepper<T> stepper);
T StandardDeviation<T>(Stepper<T> stepper);
T MeanDeviation<T>(Stepper<T> stepper);
```
### Vectors
```csharp
Vector<T> V1 = new Vector<T>(params T[] vector);
Vector<T> V2 = new Vector<T>(params T[] vector);
Vector<T> V3;
T scalar;

V3 = -V1;                   // Negate
V3 = V1 + V2;               // Add
V3 = V1 - V2;               // Subtract
V3 = V1 * scalar;           // Multiply
V3 = V1 / scalar;           // Divide
scalar = V1.DotProduct(V2); // Dot Product
V3 = V1.CrossProduct(V2);   // Cross Product
V1.Magnitude;               // Magnitude
V3 = V1.Normalize();        // Normalize
bool equal = V1 == V2;      // Equal
```
### Matrices
```csharp
Matrix<T> M1 = new Matrix<T>(int rows, int columns);
Matrix<T> M2 = new Matrix<T>(int rows, int columns);
Matrix<T> M3;
Vector<T> V2 = new Vector<T>(params T[] vector);
Vector<T> V3;
T scalar;

M3 = -M1;                               // Negate
M1 + M2;                                // Add
M3 = M1 - M2;                           // Subtract
M3 = M1 * M2;                           // Multiply
V3 = M1 * V2;                           // Multiply (vector)
M3 = M1 * scalar;                       // Multiply (scalar)
M3 = M1 / scalar;                       // Divide
M3 = M1 ^ 3;                            // Power
scalar = M1.Determinent();              // Determinent
M3 = M1.Minor(int row, int column);     // Minor
M3 = M1.Echelon();                      // Echelon Form (REF)
M3 = M1.ReducedEchelon();               // Reduced Echelon Form (RREF)
M3 = M1.Inverse();                      // Inverse
M1.DecomposeLowerUpper(ref M2, ref M3); // Lower Upper Decomposition
bool equal = M1 == M2;                  // Equal
```
### Symbolic Mathematics
```csharp
// From Linq Expression
Expression<Func<double, double>> exp1 = (x) => 2 * (x / 7);
Symbolics.Expression symExp1 = Symbolics.Parse(exp1);
Symbolics.Expression simplified = symExp1.Simplify(); // Simplification
symExp1.Substitute("x", 5);                           // Variable Subsitition

// From String
Symbolics.Expression symExp2 = Symbolics.Parse("2 * (x / 7)");
Symbolics.Expression simplified = symExp2.Simplify(); // Simplification
symExp2.Substitute("x", 5);                           // Variable Subsitition
```
## Measurement Mathematics

Towel has measurement types to provide type-safe measurement mathematics with automatic unit conversion. Never make a unit conversion mistake again, and add a layer of mathematical validation to your code.
```csharp
// Automatic Unit Conversion Example:
Angle<double> angle1 = new Angle<double>(90d, Angle.Units.Degrees);
Angle<double> angle2 = new Angle<double>(.5d, Angle.Units.Turns);
Angle<double> result1 = angle1 + angle2; // 270° 
// When you perform mathematical operations on measurements, any necessary unit conversions will
// be automatically performed by the relative measurement type (in this case "Angle<T>").

// Type Safeness Example:
Length<double> length1 = new Length<double>(2d, Length.Units.Yards);
object result2 = angle1 + length1; // WILL NOT COMPILE!!!
// The type safe-ness of the measurement types prevents the miss-use of the measurements. You cannot
// add "Length<T>" to "Angle<T>" because that is mathematically invalid (no operator exists).
```
## Data Structures

Towel has many useful data structure. Especially the Omnitree, which is an SPT that work on any number of dimensions. It can be used to make a quadtree, octree, or SPT's with higher dimensions.
```csharp
Heap<T> heap;
AvlTree<T> avlTree;
RedBlackTree<T> redBlackTree;
Omnitree<T, A1, A2, ... AX> omnitree; // (Quadtree, Octree, ...)
Tree<T> tree;
Graph<T> graph;
```
## Algorithms
```csharp
// Sorting
Sort.Shuffle<T>(...);
Sort.Bubble<T>(...);
Sort.Selection<T>(...);
Sort.Insertion<T>(...);
Sort.Quick<T>(...);
Sort.Merge<T>(...);
Sort.Heap<T>(...);
Sort.OddEven<T>(...);

// Path Finding
// Note: overloads for both Greedy and A* algorithms
Search.Graph<NODE, NUMERIC>(...);
```
## Extensions
```csharp
// System.Random extensions to generate more random types
// Note: there are overloads to specify possible ranges
string NextString(this Random random, int length);
char NextChar(this Random random);
decimal NextDecimal(this Random random);
DateTime DateTime(this Random random);
TimeSpan TimeSpan(this Random random);
long NextLong(this Random random);

// Type conversion to string as appears in C# source code
// Note: useful for runtime compilation from strings
string ConvertToCsharpSource(this Type type);
// Example typeof(List<int>) -> "System.Collections.Generic.List<int>"

string ToEnglishWords(this decimal @decimal);
// Example: 12 -> "Twelve"
```
## Developer(s)

You can chat the the developer(s) in Discord:

Discord <a href="https://discord.gg/4XbQbwF"><img src="https://discordapp.com/assets/f8389ca1a741a115313bede9ac02e2c0.svg" width="30" height="30" title="Discord" alt="Discord"></a>

 - Zachary Patten
   - sevenix.zp@gmail.com

Howdy! I'm Zachary Patten. I like making code frameworks and teaching people how to code. I only work on Towel in my free time, but feel free to contact me if you have questions and I will respond when I am able. :)
