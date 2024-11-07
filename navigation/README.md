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

A Screen something that has a compsable that renders UI content on the device's screen.
