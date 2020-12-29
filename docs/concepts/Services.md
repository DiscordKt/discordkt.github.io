Services contain and share your business logic between each of. For example, we can create a `MathService` to apply common calculations.

```kotlin
@Service
class MathService {
    fun add(a: Int, b: Int) = a + b
    fun sub(a: Int, b: Int) = a - b
    fun mult(a: Int, b: Int) = a * b
    fun div(a: Int, b: Int) = a / b
}
```

 To create a service, annotate a class with `@Service`. To use it, accept it as a parameter. This can be done anywhere you might need it, such as CommandSets, Preconditions, Listeners, and even other Services. It will automatically be given wherever it is requested.

```kotlin
@Service
class A

@Service
class B(val a: A)
```

In this case, an instance of `class A` is created, then used to create an instance of `class B`. Each of which can be used further.
