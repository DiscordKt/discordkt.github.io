Menus represent an embed message with multiple pages.

```kotlin
respondMenu {
    page {
        title = "Page 1"
    }

    page {
        title = "Page 2"
    }

    reaction(Emojis.rainbow) {
        color = genRandomColor()
    }
}
```

This creates an embed message two pages and. Two reactions are added by default in order to navigate left and right. These are standard emoji arrows, but can be changed.

You can also configure your own reactions with custom behavior. In this example, the rainbow emoji is added to the menu, and changes the color of the current page when pressed.
