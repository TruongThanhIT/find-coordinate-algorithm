# find-coordinate-algorithm
Given 3 points with the coordinate (x , y), write an efficient solution in Kotlin to find the fourth point’s coordinate so that 4 points will make a rectangle. 

# Solutions 
- Step 1: Prove three coordinates are a part of a right triangle
- Step 2: Find root square 
- Step 3: Find the midpoint hypotenuse 
- Step 4: Find the fourth coordinate

# Coding

```
import kotlin.math.pow

fun main() {
    val points =
        arrayOf(intArrayOf(1, 4), intArrayOf(3, 4), intArrayOf(3, 10)) // Expected > [1, 10]
    println("${solution(points).contentToString()}")
}

fun solution(input: Array<IntArray>): IntArray {
    val a = input[0]
    val b = input[1]
    val c = input[2]
    val ab = (a[0] - b[0]).toDouble().pow(2) + (a[1] - b[1]).toDouble().pow(2)
    val ac = (a[0] - c[0]).toDouble().pow(2) + (a[1] - c[1]).toDouble().pow(2)
    val bc = (b[0] - c[0]).toDouble().pow(2) + (b[1] - c[1]).toDouble().pow(2)
    return when {
        isRightTriangle(ab, ac, bc) -> {
            // bc is hypotenuse -> a is squareRoot
            getFinalPoint(b, c, a)
        }
        isRightTriangle(ab, bc, ac) -> {
            //  ac is hypotenuse -> b is squareRoot
            getFinalPoint(a, c, b)
        }
        else -> {
            //  ab is hypotenuse -> c is squareRoot
            getFinalPoint(a, b, c)
        }
    }
}

fun getFinalPoint(
    firstCoordinates: IntArray,
    secondCoordinates: IntArray,
    squareRoot: IntArray
): IntArray {
    val xMid = (firstCoordinates[0] + secondCoordinates[0]) / 2
    val yMid = (firstCoordinates[1] + secondCoordinates[1]) / 2
    val xFinal = (xMid * 2) - squareRoot[0]
    val yFinal = (yMid * 2) - squareRoot[1]
    return intArrayOf(xFinal, yFinal)
}

fun isRightTriangle(
    firstAngle: Double,
    secondAngle: Double,
    hypotenuse: Double
): Boolean = ((firstAngle + secondAngle) == hypotenuse)

```
