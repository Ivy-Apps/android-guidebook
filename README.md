# Android Guidebook

> A no-nonsense, opinionated collection of hard-earned lessons from 8 years of Android development—as a founding engineer at four startups and a contractor at Toptal and Reddit.

Android development isn’t just about cranking out code; it’s a branch of **software engineering**, and like any engineering discipline, it’s grounded in **science**. Beneath every library, framework, and pattern lies a foundation of **mathematics** and **formal logic**.

This guidebook isn’t here to just teach you how to use tools; it’s here to challenge you to **think like an engineer**. Together, we’ll dissect Android development through the lens of scientific principles—arming you with the knowledge to not just follow best practices but to deeply understand and, when necessary, improve upon them.

> [!TIP]
> Become a better software engineer. Learn algorithms, data structures, architecture and software design from first principles... [ivylearn.app](https://ivylearn.app/) ✨

## Why Should I Care?

![Hype Train](./hype-train.webp)

Modern Android Development often feels like an endless ride on the **hype train**: every year brings flashy new libraries and practices, while last year’s tools are quickly deprecated. It’s easy to get caught up in this cycle, chasing trends without digging into the real engineering beneath the surface.

But here’s the thing: the shiny stuff won’t last. Instead of memorizing the latest APIs (that’ll be obsolete soon anyway), let’s dive deeper. This guidebook focuses on **re-discovering and re-inventing** the fundamental principles and technologies that power those shiny tools.

Why reinvent the wheel? Because it’s the best way to step into the shoes of library and API creators. Only then can you truly grasp their design choices—their trade-offs, limitations, and, most importantly, their **why**.

> [!TIP]  
> Mastery is when you can “rebuild it from scratch if left alone in a basement without internet for a week.” Only then will you wield these tools with confidence—and who knows, you might invent something better.

This guidebook won’t just skim the surface of new trends. It’s about going back to **first principles**, understanding them deeply, and making Android development feel straightforward—even boring. By the end, building complex Android or Kotlin Multiplatform apps should feel trivial, not overwhelming.

> [!NOTE]  
> Before we jump into the exciting parts, we need to establish a shared understanding of the formal language and core concepts that will guide us through this journey.

## Topics
- [Navigation](/navigation/README.md)
- [Modularization]() 🚧
- [Unit Testing]() 🚧
- [Property-based Testing]() 🚧
- [CI & CD]() 🚧
- [Data Layer]() 🚧
- [Domain Layer]() 🚧
- [UI Layer]() 🚧
- [Scaling Architecture]() 🚧
- [MVI]() 🚧
- [Efficient Compose UI]() 🚧
- [Screenshot testing UI]() 🚧
- [Dependency Injection (DI)]() 🚧
- [Idiomatic Kotlin for expressing complex logic elegantly]() 🚧
- [Gradle Build system]() 🚧
- [Android Studio Live Templates]() 🚧
- [Centralize your dependencies with a version catalog]() 🚧

> [!TIP]  
> To get the most out of this guidebook, make sure you're familiar with some foundational concepts: **implication**, **equivalence**, **sets**, and the basics of **formal logic** and **mathematics**. If any of these sound unfamiliar, no worries—just stick around and read through to the end. Best case? You’ll pick up something new. Worst case? You’ll reinforce what you already know and feel even more confident.

> *🚧 means that topic is under construction and is not read, yet

# Formal language 

## Implications

An implication is a one-way logical statement that takes the form "if P, then Q", often written as **P ⇒ Q** (P implies Q). Here:

- **P** is the cause or assumption (what's the condition).
- **Q** is the result (what follows if P is true).

Think of it this way: "If it rains, then the ground gets wet." In logical terms, this is **P ⇒ Q** where:

- **P**: "It rains."
- **Q**: "The ground gets wet."

> **P ⇒ Q** is read as _P: "It rains" implies that Q: "The ground gets wet"._

This means if it's raining, we can be sure that the ground is wet. However, the reverse isn't always true: if the ground is wet, it doesn't guarantee it has rained—it could be wet for other reasons, like a sprinkler system.

So, an implication is one-way: **P ⇒ Q** does not mean **Q ⇒ P**. This is a key part of formal logic that helps build precise reasoning.

> [!IMPORTANT]
> Implications are neither good or bad, they are merely facts: from **Cause** follows **Effect**. This makes them suitable for discussing technical approaches because compared to Pros/Cons or Benefits/Drawbacks, implications aren't subjective nor biased.

## Sets

A set is a collection of unique objects (items) that isn't ordered. Symbolically, sets are denoted with uppercase letters and curly braces. For example: `A = {1, 2, 3}`, `M = { "World", "Hello",}`.

**Set key properties**

1. Order doesn’t matter:
- `{1, 2, 3} = {3, 2, 1}`

2. An item can't be repeated/duplicated:
- `{A, B, C} + B = {A, B, C}`

## Properties

A property is a set of implications defining characteristic of an object or concept. When an object has a property, specific conclusions follow, allowing us to precisely define its behavior or characteristics.

### Example 1: Square
**Property**: Being a square.

#### Implications:

1. If a shape is a square, all four sides are equal in length:
   - **P**: Shape is a square ⇒ **Q**: All sides are equal

2. This property also implies that each internal angle is 90 degrees:
   - **P**: Shape is a square ⇒ **R**: Each angle is 90°

3. Additionally, a square remains unchanged if rotated by 90°, 180°, or 270°:
   - **P**: Shape is a square ⇒ **S**: Rotation by 90°, 180°, or 270° leaves it unchanged

These implications show that knowing a shape is a square allows us to logically derive its specific attributes and symmetry properties. 

> [!NOTE]
> From a property we can derive and prove more implications (e.g. being a square implies having equal diagonals). In other words, a property defines a set of implications that are guaranteed to be true but that doesn't stop us from expanding this set with more implications.

### Example 2: Reactivity in Jetpack Compose

**Property**: Reactivity in Jetpack Compose.

#### Implications

1. If a variable is a reactive `State`, any change in its value triggers recomposition in any Composable that reads it:
   - **P**: Variable is a reactive `State` ⇒ **R**: Composable reading this `State` recomposes on value change

2. If multiple Composables read the same reactive `State`, any change in that `State` triggers recomposition in each dependent Composable:
   - **P**: Reactive `State` value changes ⇒ **DR**: All dependent Composables recompose

3. If a Composable reads multiple reactive `State` values, only the parts of the UI that depend on each specific `State` recompose when that `State` changes, optimizing rendering performance:
   - **P**: Composable reads multiple reactive `States` ⇒ **A**: Only affected parts of the UI recompose on specific `State` change

These implications allow for precise control and prediction of UI behavior in Compose when working with reactive `State` in Compose.

> [!TIP]
>  Properties provide precise and explicit definitions of behavior through implications. Having formal language and mathematical rigor in place, let's us use formal logic to derive more implications and analyze our approaches. This is a step further than arguing whether the solution is KISS (Keep It Simple Stupid) or DRY (Don't Repeat Yourself).

## Equivalence

Equivalence means two statements or properties imply each other within a given context, even if they aren’t identical in every aspect. We write this as **A ⇔ B**, meaning **A** implies **B** and **B** implies **A**. Equivalence does not mean the two things are the same; rather, it indicates that they share key behaviors or properties within specific boundaries.

### Example: Rain and Wet Sidewalk

Let's consider a familiar scenario to illustrate equivalence:

**Context**: In a small town without sprinklers, street cleaning, or other sources of water, the only way the sidewalk becomes wet is when it rains.

**Properties and Implications**:

1. **Property**: If it rains, the sidewalk becomes wet:
   - **P**: "It rains" implies **Q**: "The sidewalk is wet" (P ⇒ Q).

2. **Property**: If the sidewalk is wet, it must have rained:
   - **Q**: "The sidewalk is wet" implies **P**: "It rains" (Q ⇒ P).

**Equivalence**:

Since both **P ⇒ Q** and **Q ⇒ P** hold, we establish **P ⇔ Q**:

- **P ⇔ Q**

This equivalence means that "It rains" and "The sidewalk is wet" share the same implications within this context; they occur together, making each statement true if and only if the other is also true.

> [!IMPORTANT]
> **Changing Context**:
>
> If we consider a city where sprinklers or street cleaning exist, the sidewalk could become wet without rain. In this context, **Q** (the sidewalk is wet) no longer implies **P** (it is raining), and the equivalence no longer holds.

This example shows how equivalence depends on specific properties and context, allowing us to understand when two statements are logically linked such that one being true guarantees the other is also true.


### Proof of Behavioral Equivalence: Compose State and StateFlow in Jetpack Compose Reactivity

**Context:** Examining reactivity in Jetpack Compose — how changes in state values trigger recomposition in observing Composables.

**Definitions:**

1. **Reactivity Property (R):** A change in state value triggers recomposition in any Composable observing that state.

2. **Compose `State<T>` (S):** A state holder that triggers recomposition when its value changes.

3. **`StateFlow<T>` (F):** A flow that, when collected via collectAsState(), triggers recomposition on new emissions.


**Implications:**

**S ⇒ R:** Changes in `State<T>` trigger recomposition.

**F ⇒ R:** Emissions from `StateFlow<T>` collected via collectAsState() trigger recomposition.

**Behavioral Equivalence Statement:**

Since both `State<T>` and `StateFlow<T>` satisfy the reactivity property **R** and their behaviors are indistinguishable to observing Composables, they are behaviorally equivalent in this context:

**S ≅ F** (**S** is behaviorally equivalent to **F**) with respect to reactivity in Jetpack Compose.

**Code Demonstration:**
```kotlin
// StateFlow to Compose State
@Composable
fun <T> StateFlow<T>.toComposeState(): State<T> {
  return this.collectAsState()
}

// Compose State to StateFlow
@Composable
fun <T> State<T>.toStateFlow(): StateFlow<T> {
  val flow = remember { MutableStateFlow(this.value) }
  LaunchedEffect(this.value) {
    flow.value = this.value
  }
  return flow
}
```

**Conclusion:**

**Behavioral Equivalence:** `State<T>` and `StateFlow<T>` are behaviorally equivalent in the context of reactivity in Jetpack Compose and we can use them interchangeably.

> [!TIP]
> **In Practice**
> 
> We'll use **S ≅ F in C** (behavioral equivalence between S and F in context C) a lot because it'll allow us to find equivalent solutions and then optimize for what we need: e.g. simplicity, performance, type-safety.
> 1. Find a set of equivalent solutions
> 2. Rank them by the properties that we care about.

## Quantifiers

In programming we often work with collections or need to analyze multiple possible cases. To be able to communicate effectively and prove that our programs work we need a formal way to reason about quantities.

### **∀** for all

**∀** (every) states that some property holds for all possible values in the set.
- **(∀n∈Int: n < Int.MAX_VALUE/2)(x=2*n ⇒ x even number)**
- Every integer **n** that is smaller than Int.MAX_VALUE/2 when multiplied by 2 is an even number.

**∀(a,b∈{1,2,3})** implies that a, b can be all possible permutations of two numbers picked from {1,2,3}, precisely:
- (1,1), (1,2), (1,3)
- (2,1), (2,2), (2,3)
- (3,1), (3,2), (3,3)

**∀(first, middle, last ∈ {"John","Doe"})**:
- "John John John", "John John Doe", "John Doe John", "John Doe Doe"
- "Doe Doe Doe", "Doe Doe John", "Doe John Doe", "Doe John John"

  
### **∃** there exists

**∃** (exists) states that there is at least one value in the set that satisfy some property.
- **(∃n∈Int: n < 10)(n+n = n*n)**
- There exists an integer **n** that is smaller than 10, such that **n+n=n*n**.
- _(in this example such integer is 2 because 2+2=2*2)_

**∄ (there does not exist)** states that there is no such value that satisfies some property or conditions.
- **(∄n∈Int)[n*2 is odd]**
- There does not exist an integer **n** that when multiplied by 2 is an odd number.

### Combining Quantifiers

```kotlin
fun hourlyRate(monthlyUsd: Double, hours: Int): Double {
  return monthlyUsd / hours
}
```
- **(∀monthlyUsd∈Double)(∃hours∈Int)[hourlyRate(monthlyUsd, hours) ⇒ runtime exception]**
- For every double `monthlyUsd`, there exists a `hours` integer that will make the `hourlyRate` function throw a runtime exception.
- This can happen for **hours = 0**.

> [!TIP]
> Quantifiers are chained from left to right. You can treat them as nested `for` loops where the first quantifier surrounds the second one and so on. For example, **(∀a∈Int)(∀b∈Int: b != a)(∃x∈Double)(a > x > b)** means "for every integer **a** and for every intereger **b** that is different from **a**, there exists a double **x** that is between **a** and **b**".

## Wrapping up...

That’s mostly what we need from formal mathematical language and logic to get started with the engineering topics. If you want to dive deeper, I highly recommend checking out the free [Introduction to Mathematical Thinking course](https://www.coursera.org/learn/mathematical-thinking) by Dr. Keith Devlin from Stanford University. It’s an excellent resource to sharpen your reasoning skills.

---

# [🚀 Let's go!](https://ivylearn.app)

If you like such content, I got something better for you - [Ivy Learn](https://ivylearn.app) ✨️

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Ivy-Apps/android-guidebook&type=Date)](https://star-history.com/#Ivy-Apps/android-guidebook&Date)
