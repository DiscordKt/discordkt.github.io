Menus represent an embed message with multiple pages.

```kotlin
respondMenu {
    page {
        title = "Page 1"
    }

    page {
        title = "Page 2"
    }

    buttons {
        button("Left", Emojis.arrowLeft) {
            previousPage()
        }

        button("Right", Emojis.arrowRight) {
            nextPage()
        }

        editButton("Rainbow", Emojis.rainbow) {
            color = genRandomColor()
        }
    }
}
```

This creates an embed message with two buttons for navigation, and one button for editing the current embed.
