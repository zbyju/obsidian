# RT Function
```scala
// 0.
def add(a: Int, b: Int): Int = a + b
// 1.
val result = add(5, 3)
// 2.
val result = 5 + 3
// 3.
val result = 8
```
We would get the same result every time we would run this program.

# Non-RT Function
```scala
// 0.
def randomNumber(): Int = scala.util.Random.nextInt()
// 1.
val result = randomNumber()
// 2.
val result = 4
// 2.
val result = 8
```

[[Substitution Model]]