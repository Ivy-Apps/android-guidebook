# Android Guidebook

> An opinionated collection of learnings from my Android experience as a founding engineer in 4 startups and a contractor at Toptal and Reddit.

Android Development is, before all, software engineering, which, like any engineering field, is based on science. And when it comes to science, math, and formal logic rule the game. So in this guidebook, we'll look into the Android Development and software engineering best practices through the lens of science.

So before we begin, we need to get familiar with the formal language.

## Formal language

### Implications

An **implication** is a one-way logical statement that takes the form "if P, then Q", often written as `P ⇒ Q`. Here:

- P is the **cause** or **assumption** (what we start with).
- Q is the **result** (what follows if P is true).

Think of it this way: "If it rains, then the ground is wet." In logic terms, this is `P ⇒ Q` where:

- P: "It rains."
- Q: "The ground is wet."

This means if it’s raining, we can be sure the ground is wet. However, the reverse isn’t always true: if the ground is wet, it doesn’t guarantee it has rained—it could be a sprinkler or someone washing the street.

So, an implication is one-way: `P ⇒ Q` does not mean `Q ⇒ P`. This is a key part of formal logic that helps build precise reasoning.

### Properties

A **property** is a defining characteristic of an object or concept that brings a set of **implications**. When an object has a property, certain logical conclusions follow from it, allowing us to precisely define its behavior or characteristics.

#### Example 1: Equilateral Triangle

**Property**: The property of being an **equilateral triangle**.

- **Implications**:
  - If a triangle has the property of being equilateral, it implies all three sides are equal in length:
  
    ```
    P: Triangle is equilateral ⇒ Q: All sides are equal
    ```

  - This property also implies that each angle in the triangle is 60 degrees:
  
    ```
    P: Triangle is equilateral ⇒ R: Each angle is 60 degrees
    ```

  - Additionally, if we rotate an equilateral triangle by 120 degrees or 240 degrees, it remains identical due to its symmetry:
  
    ```
    P: Triangle is equilateral ⇒ S: Rotation by 120° or 240° leaves it unchanged
    ```

These implications mean that knowing a triangle is equilateral lets us derive specific, logical attributes about its structure and behavior.

#### Example 2: Reactivity in Jetpack Compose

**Property**: The property of **reactivity** in Jetpack Compose with `State` and `Flow`.

- **Implications**:
  - If a variable is declared as a `State`, then any change to its value will automatically trigger a re-composition of any UI component reading this state:
  
    ```
    P: Variable is a State in Compose ⇒ Q: UI component recomposes on value change
    ```

  - If a `Flow` emits a new value and is collected in a Composable, the UI component will update according to the emitted value:
  
    ```
    P: Flow emits new value ⇒ Q: Collected Composable updates with new data
    ```

  - If a Composable function reads multiple `State` values, any change in those values will lead to recomposition only of the parts that depend on the changed states, optimizing performance:
  
    ```
    P: Composable reads multiple States ⇒ Q: Recomposition occurs only for affected parts
    ```

In these examples, each property enables us to understand the behavior and characteristics of an object formally and logically, allowing precise control and prediction in development.

### Equivalence

**Equivalence** means two things imply each other in a given context, even if they aren’t identical. We write this as `A ⇔ B`, meaning **A implies B and B implies A**. Equivalence doesn’t mean two things are the same; instead, they share key behaviors or properties **within specific bounds**.

#### Example: Rain and Wet Ground

Imagine a sealed greenhouse where the only water source is rain:

- If it rains, the ground becomes wet:

P: It rains ⇒ Q: The ground is wet

- If the ground is wet, it must have rained (since there’s no other water source):

Q: The ground is wet ⇒ P: It rains

Here, `P ⇔ Q` because each implies the other in the greenhouse context. Outside this context (e.g., where sprinklers exist), this equivalence would no longer apply.

### Proof of Equivalence: `MutableStateFlow` and `MutableState` up to Reactivity

In Jetpack Compose, we can show that `MutableStateFlow` and `MutableState` are **equivalent up to reactivity** by proving that each one implies the same reactivity behavior in UI recomposition.

#### Definitions

- **Reactivity Property**: A state’s change triggers recomposition of any Composable observing it.

#### Implications

1. **`MutableStateFlow` implies reactivity**:
   - When a `MutableStateFlow` emits a new value, any Composable collecting it updates:
   
     ```
     F: MutableStateFlow emits new value ⇒ C: Collected Composable updates
     ```

2. **`MutableState` implies reactivity**:
   - When a `MutableState` changes, any Composable reading this state recomposes:
   
     ```
     M: MutableState changes ⇒ C: Reading Composable updates
     ```

#### Equivalence Statement

Since `MutableStateFlow` and `MutableState` each imply UI recomposition in Jetpack Compose, we conclude:

F ⇔ M up to reactivity in Compose

Thus, `MutableStateFlow` and `MutableState` are **equivalent up to the reactivity property** within the Compose framework, meaning they can be used interchangeably for triggering UI recomposition, though they remain distinct in other behaviors.
