# Jetpack Compose
Instagram Stories using Jetpack Compose

![alt text](https://github.com/jorgecasariego/instagram-story-compose/blob/main/Demo/demo2.gif?raw=true)

## What is Jetpack Compose?
Jetpack compose is a modern Android UI toolkit introduced by Google. It simplifies the app development process and speeds it up. With Jetpack Compose, you can write less code compared to the current view building approach – which also means less potential bugs. There is one more great thing about it – it uses Kotlin.

## The state
Updating a view is a crucial task of every single application. It’s hard to imagine the app which shows you the same data all the time. To update a view in Compose, we need to rebuild Composable functions with different sets of arguments.

This process is called recomposition. The question is “How does a Composable function know when to rebuild itself?”. The answer is – because it can have a state. 

The state is a value, or multiple values, assigned to a Composable function. Whenever the value is changed, it triggers a recomposition process and our composable function will be rebuilt with a new state value.

```Kotlin
    val currentStep = remember { mutableStateOf(0) }
    val isPaused = remember { mutableStateOf(false) }
    
    BoxWithConstraints(modifier = Modifier.fillMaxSize()) {
        val imageModifier = Modifier
            .fillMaxSize()
            .pointerInput(Unit) {
                detectTapGestures(
                    onTap = { offset ->
                        currentStep.value = if (offset.x < constraints.maxWidth / 2) {
                            max(0, currentStep.value - 1)
                        } else {
                            min(stepCount - 1, currentStep.value + 1)
                        }
                    },
                    onPress = {
                        try {
                            isPaused.value = true
                            awaitRelease()
                        } finally {
                            isPaused.value = false
                        }
                    }
                )
            }
```
