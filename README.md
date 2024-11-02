# Android Guidebook

> An opinionated collection of learnings through my 8 years of Android experience as a founding engineer in four startups and a contractor at Toptal and Reddit.

Android Development is above all software engineering, which, like any engineering field, is based on science. When it comes to science, math and formal logic rule the game. In this guidebook, we'll look into Android Development and software engineering through the lens of science.

> [!NOTE]
> Before we begin, we need to get familiar with the formal language so we can communicate effectively instead of debating what's a best practice or an anti-pattern based on arbitrary articles and opinions.

## Topics
- [Navigation]()
- [Modularization]()
- [Unit Testing]()
- [Property-based Testing]()
- [CI & CD]()
- [Data layer]()
- [Domain layer]()
- [UI layer]()
- [MVI]()
- [Efficient Compose UI]()
- [Screenshot testing UI]()
- [Dependency Injection (DI)]()
- [Idiomatic Kotlin for expressing complex logic elegantly]()

# Formal language 

## Implications

An implication is a one-way logical statement that takes the form "if P, then Q", often written as **P ⇒ Q** (P implies Q). Here:

- **P** is the cause or assumption (what's the condition).
- **Q** is the result (what follows if P is true).

Think of it this way: "If it rains, then the ground gets wet." In logical terms, this is **P ⇒ Q** where:

- **P**: "It rains."
- **Q**: "The ground gets wet."

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

These implications show that knowing a shape is a square allows us to logically derive its specific attributes and symmetry properties. Of course, from the above implications we can derive more implications (e.g. being a square implies having equal diagonals).

### Example 2: Reactivity in Jetpack Compose

**Property**: Reactivity in Jetpack Compose.

#### Implications

1. If a variable is a reactive `State`, any change in its value triggers recomposition in any Composable that reads it:
   - **P**: Variable is a reactive `State` ⇒ **Q**: Composable reading this `State` recomposes on value change

2. If multiple Composables read the same reactive `State`, any change in that `State` triggers recomposition in each dependent Composable:
   - **P**: Reactive `State` value changes ⇒ **Q**: All dependent Composables recompute

3. If a Composable reads multiple reactive `State` values, only the parts of the UI that depend on each specific `State` recompose when that `State` changes, optimizing rendering performance:
   - **P**: Composable reads multiple reactive `States` ⇒ **Q**: Only affected parts of the UI recompute on specific `State` change

These implications allow for precise control and prediction of UI behavior in Compose when working with reactive `State`.

> [!TIP]
>  Working with properties allows for precise and explicit definitions of behavior through implications. Having formal language and mathematical rigor in place, let's use logic to derive more implications and analyze our approaches. This is a step further than arguing whether the solution is KISS (Keep It Simple Stupid) or DRY (Don't Repeat Yourself).

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

### Proof of Equivalence: `MutableState` and `MutableStateFlow` in terms of Reactivity in Jetpack Compose

In Jetpack Compose, both `MutableState` and `MutableStateFlow` exhibit reactivity. We demonstrate their equivalence by showing that each implies the same reactivity property in UI recomposition.

**Definitions and Reactivity Property**

1. **Reactivity Property**: A change in a state value triggers recomposition in any Composable observing that state.

**Implications of `MutableState`**

1. **Property**: If a variable is defined as `MutableState`, then any change in its value triggers recomposition of any Composable reading this `State`.
   - **M**: "Variable is a `MutableState`" implies **C**: "Composable observing it recomposes on change" (M ⇒ C).

2. **Property**: If a Composable recomposes due to observing a state, that state could be defined as `MutableState`.
   - **C**: "Composable recomposes on state change" implies **M**: "State is a `MutableState`" (C ⇒ M).

**Implications of `MutableStateFlow`**

1. **Property**: If a variable is defined as `MutableStateFlow`, any emission of a new value triggers recomposition in any Composable collecting it.
   - **F**: "Variable is a `MutableStateFlow`" implies **C**: "Composable observing it recomposes on new emission" (F ⇒ C).

2. **Property**: If a Composable recomposes due to a state change, that state could be defined as `MutableStateFlow`.
   - **C**: "Composable recomposes on state change" implies **F**: "State is a `MutableStateFlow`" (C ⇒ F).

**Equivalence Statement**

Since both `MutableState` and `MutableStateFlow` imply the same reactivity property in Jetpack Compose (that any state change triggers recomposition of dependent Composables), we conclude that within the context of reactivity in Compose:

- **M ⇔ F**

Thus, `MutableState` and `MutableStateFlow` are equivalent in terms of their reactivity behavior in Compose. This equivalence holds specifically within the Compose framework, where both types ensure UI recomposition in response to state changes, though they may differ in other aspects outside this context.
