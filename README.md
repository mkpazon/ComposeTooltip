![Sample app screenshot](https://github.com/skgmn/ComposeTooltip/blob/master/.github/images/sample_screenshot.png)

# Setup

```gradle
implementation "com.github.skgmn:composetooltip:0.1.0"
```

# Usage

## Basic example

```kotlin
ConstraintLayout {
    val someImage = createRef()
    Image(
        painter = painterResource(R.drawable.some_image),
        contentDescription = "Some image"
        modifier = Modifier.constrainAs(someImage) {
            // Place it where you want
        }
    )
    Tooltip(
        anchor = someImage,
        anchorEdge = AnchorEdge.Top,
    ) {
        Text("This is my image!")
    }
}
```

Note that `Tooltip` can only be used inside `ConstraintLayout`.

## Method signatures

```kotlin
fun ConstraintLayoutScope.Tooltip(
    anchor: ConstrainedLayoutReference,
    anchorEdge: AnchorEdge,
    modifier: Modifier = Modifier,
    tooltipStyle: TooltipStyle = rememberTooltipStyle(),
    tipPosition: EdgePosition = remember { EdgePosition() },
    anchorPosition: EdgePosition = remember { EdgePosition() },
    margin: Dp = 8.dp,
    content: @Composable RowScope.() -> Unit
)
```

* `anchor` - `ConstrainedLayoutReference` to locate this tooltip nearby
* `anchorEdge` - Can be either of `AnchorEdge.Start`, `AnchorEdge.Top`, `AnchorEdge.End`, or `AnchorEdge.Bottom`
* `tooltipStyle` - Style for tooltip. Can be created by `rememberTooltipStyle`
* `tipPosition` - Tip position relative to balloon
* `anchorPosition` - Position on the `anchor`'s edge where the tip points out.
* `margin` - Margin between tip and `anchor`
* `content` - Content inside balloon. Typically `Text`.

`Tooltip` also supports enter/exit transition using `AnimatedVisibility`. Because `AnimatedVisibility` is experimental, this method is also experimental.

```kotlin
fun ConstraintLayoutScope.Tooltip(
    anchor: ConstrainedLayoutReference,
    anchorEdge: AnchorEdge,
    enterTransition: EnterTransition,
    exitTransition: ExitTransition,
    modifier: Modifier = Modifier,
    visible: Boolean = true,
    tooltipStyle: TooltipStyle = rememberTooltipStyle(),
    tipPosition: EdgePosition = remember { EdgePosition() },
    anchorPosition: EdgePosition = remember { EdgePosition() },
    margin: Dp = 8.dp,
    content: @Composable RowScope.() -> Unit
)
```

* `enterTransition` - `EnterTransition` to be applied when the `visible` becomes true. Types of `EnterTransition` are listed [here](https://developer.android.com/jetpack/compose/animation#entertransition).
* `exitTransition` - `ExitTransition` to be applied when the `visible` becomes false. Types of `ExitTransition` are listed [here](https://developer.android.com/jetpack/compose/animation#exittransition).
