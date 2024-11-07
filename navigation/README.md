# Navigation

Navigation is essential for every Android app. 
It allows users to view different screens and surfaces within the app
and find what they need.

Navigation can become complex topic if tackled as one big chunk so we'll start
small and simple. We'll build a Compose system that can navigates between screens.

So as with every engineering problem let's start with its definition.
We mentioned the word "screen" a few times but what exactly does it mean?

> [!NOTE]
> **Definition: Screen**
> 
> A **Screen** is a user interface (UI) component that occupies the entire device viewport. As the name suggests, it takes up the whole screen, providing a focused context for user interaction.

And in code, we can define like this:
```kotlin
interface Screen {
  @Composable
  fun Content()
}
```

A Screen something that has a compsable that renders UI content on the device's screen. So far, so good!

In most apps, the user should be able to navigate back-and-forth between Screens but let's formally define what a simple navigation should be able to do.

## Navigation definition
 
**(∀app∈Android app)(∃nav∈Navigation)(∃backstack∈[Stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)))(∀s1,s2∈Screen)[**

1. *nav.backstack := [] ∧ nav.push(s1) ⇒ nav.current = s1 ∧ nav.backstack = [s1]*
2. *∀b∈Stack: nav.backstack := b ∧ nav.push(s1) ⇒ nav.current = s1 ∧ nav.backstack = b.push(s1)*
3. *nav.backstack := [s1, s2] ∧ nav.pop() ⇒ nav.current = s1 ∧ nav.backstack = [s1]*
4. *nav.backstack := [s1] ∧ nav.pop() ⇒ ¬app.isForeground ∧ nav.current = s1 ∧ nav.backstack = [s1]*
5. *nav.backstack := [] ∧ nav.pop() ⇒ ¬app.isForeground ∧ nav.current = ∅ ∧ nav.backstack = []*
6. *nav.push(s1) ∧ nav.pop() ⇔ nav*

**]**

> [!TIP]
> - **:= (Is defined to be)**: assigns value, e.g. x := 5 means we set the value of 5 to **x**
> - **= (Equal to)**: reads value, e.g. x = 5 means that **x** is equal to 5
> - **∧ (AND)**
> - **∨ (OR)**
> - **¬ (NOT)**
> - **∅ (null, undefined)**
> - **⊥ (bottom)**: computation that produces an error or goes into an infinite loop

> [!NOTE]
> **Stack:**
>
> - Stack([1, 2]).push(3) = Stack([1, 2, 3])
> - Stack([1, 2, 3]).pop() = Stack([1, 2])
> - Stack([]).pop() = ⊥
