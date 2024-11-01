# Android Guidebook

> An opinionated collection of learnings from my 8 years of Android experience as a founding engineer in 4 startups and a contractor at Toptal and Reddit.

Android Development is above all software engineering, which, like any engineering field, is based on science. When it comes to science, math and formal logic rule the game. In this guidebook, we'll look into Android Development and software engineering through the lens of science.

> [!NOTE]
> Before we begin, we need to get familiar with the formal language so we can communicate effectively instead of debating what's best practice and anti-pattern based on arbitrary articles and opinions.

## Formal Language

### Implications

An implication is a one-way logical statement that takes the form "if P, then Q", often written as **P ⇒ Q** (P implies Q). Here:

- **P** is the cause or assumption (what's the condition).
- **Q** is the result (what follows if P is true).

Think of it this way: "If it rains, then the ground gets wet." In logical terms, this is **P ⇒ Q** where:

- **P**: "It rains."
- **Q**: "The ground gets wet."

This means if it's raining, we can be sure that the ground is wet. However, the reverse isn't always true: if the ground is wet, it doesn't guarantee it has rained—it could be wet for other reasons, like a sprinkler system.

So, an implication is one-way: **P ⇒ Q** does not mean **Q ⇒ P**. This is a key part of formal logic that helps build precise reasoning.

> [!TIP]
> Implications are neither good or bad, they are merely facts. This makes them good for discussing technical approaches because compared to Pros/Cons or Benefits/Drawbacks implications aren't subjective and biased.

### Sets

A set is a collection of unique objects (items) that isn't ordered. Symbolically, sets are denoted with uppercase letters and curly braces. For example: `A = {1, 2, 3}`, `M = { "World", "Hello",}`.

#### Set key properties

1. Order doesn’t matter:
- `{1, 2, 3} = {3, 2, 1}`

2. An item can't be repeated/duplicated:
- `{A, B, C} + B = {A, B, C}`

## Properties

A **property** is a defining characteristic of an object or concept that implies certain logical consequences. When an object has a property, specific conclusions follow, allowing us to precisely define its behavior or characteristics.

### Example: Square
**Property**: Being a square.

#### Implications:

1. If a shape is a square, all four sides are equal in length:
   - **P**: Shape is a square ⇒ **Q**: All sides are equal

2. This property also implies that each internal angle is 90 degrees:
   - **P**: Shape is a square ⇒ **R**: Each angle is 90°

3. Additionally, a square remains unchanged if rotated by 90°, 180°, or 270°:
   - **P**: Shape is a square ⇒ **S**: Rotation by 90°, 180°, or 270° leaves it unchanged

These implications show that knowing a shape is a square allows us to logically derive its specific attributes and symmetry properties.

#### Example 2: Reactivity in Jetpack Compose

**Property**: Reactivity in Jetpack Compose with `State` and `Flow`.

**Implications**:

1. If a variable is declared as a `State`, any change to its value will automatically trigger a recomposition of any UI component reading this state:

   - **P**: Variable is a `State` in Compose ⇒ **Q**: UI component recomposes on value change

2. If a `Flow` emits a new value and is collected in a Composable, the UI component updates according to the emitted value:

   - **P**: `Flow` emits new value ⇒ **Q**: Collected Composable updates with new data

3. If a Composable function reads multiple `State` values, any change in those values leads to recomposition only of the parts that depend on the changed states, optimizing performance:

   - **P**: Composable reads multiple `States` ⇒ **Q**: Recomposition occurs only for affected parts

In these examples, each property enables us to understand the behavior and characteristics of an object formally and logically, allowing precise control and prediction in development.

### Equivalence

Equivalence means two statements imply each other within a given context, even if they aren’t identical in every aspect. We write this as **A ⇔ B**, meaning **A** implies **B** and **B** implies **A**. Equivalence doesn't mean the two things are the same; instead, they share key behaviors or properties within specific boundaries.

#### Example: Rain and Wet Sidewalk

Let's consider a familiar scenario to illustrate equivalence:

**Context**: In a small town where there are no sprinklers, street cleaning, or any other sources of water that can wet the sidewalk. The only way the sidewalk gets wet is when it rains.

**Implications**:

1. If it is raining, then the sidewalk is wet:

   - **P**: It is raining ⇒ **Q**: The sidewalk is wet

   This means that rain causes the sidewalk to become wet.

2. If the sidewalk is wet, then it is raining:

   - **Q**: The sidewalk is wet ⇒ **P**: It is raining

   In this context, since there's no other way for the sidewalk to get wet, a wet sidewalk implies that it's raining.

**Equivalence**:

Since both **P** implies **Q** and **Q** implies **P**, we have an equivalence:

- **P ⇔ Q**

This means "It is raining" and "The sidewalk is wet" are equivalent in this context—they always occur together.

> [!IMPORTANT]
> **Changing the Context**:
>
> If we consider a city where sprinklers or street cleaning exist, the sidewalk could be wet without rain. In this new context, **Q** (the sidewalk is wet) does not necessarily imply **P** (it is raining) anymore, and the equivalence no longer holds.

This example shows how equivalence depends on context and helps us understand that two different statements can be logically linked such that one being true guarantees the other is true, and vice versa, within specific boundaries.

#### Proof of Equivalence: `MutableStateFlow` and `MutableState` up to Reactivity

In Jetpack Compose, we can demonstrate that `MutableStateFlow` and `MutableState` are equivalent up to reactivity by showing that each one implies the same reactivity behavior in UI recomposition.

**Definitions**

- **Reactivity Property**: A state’s change triggers recomposition of any Composable observing it.

**Implications**

1. **`MutableStateFlow` implies reactivity**:

   When a `MutableStateFlow` emits a new value, any Composable collecting it updates:

   - **F**: `MutableStateFlow` emits new value ⇒ **C**: Collected Composable updates

2. **`MutableState` implies reactivity**:

   When a `MutableState` changes, any Composable reading this state recomposes:

   - **M**: `MutableState` changes ⇒ **C**: Reading Composable updates

**Equivalence Statement**

Since `MutableStateFlow` and `MutableState` each imply the same reactivity behavior in Jetpack Compose, we conclude:

- **F ⇔ M** (up to reactivity in Compose)

This means that, concerning reactivity within the Compose framework, `MutableStateFlow` and `MutableState` are equivalent—they can be used interchangeably for triggering UI recomposition, though they remain distinct in other behaviors.
