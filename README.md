# Obsidian Canvas Snippets

Here is a list of useful snippets to improve Obsidian Canvas.  
I will add more as I create them.  
Don't forget to share & star 🙂

## Canva Node Icons
![image](https://github.com/ShahriarKh/obsidian-canvas-snippets/assets/31452340/e7bf311f-94fe-4725-829d-239b6ee1cd74)

### Snippet
Add this css snippet. Feel free to change padding, margin and others based on your theme styles.
```css
.canvas-node:not(.is-editing) {
  .ni {
    padding: 4px; /* feel free to change based on your theme styles */
    position: absolute;

    &[data-icon] {
      &:before {
        display: block;
        content: attr(data-icon);
      }

      /* feel free to change based on your theme styles */
        font-family: "Segoe UI Emoji"; /* change this to an emoji font that matches your system */
        font-size: 1rem;
        padding: 0; 
    }

    /* feel free to change based on your theme styles */
    &.t {
      top: 0;
    }

    &.b {
      bottom: 0;
    }

    &.r {
      right: -12px;
    }

    &.l {
      left: 0;
    }
  }
}

```

### Usage
Add one or more spans to your node. `ni` (short for "node icon") is required.
Use `t` (top), `l` (left), `r` (right), `b` (bottom) classes for positioning.

Use `data-icon="⭐"` if you want to use an emoji.  
You can use [Obsidian Iconize Plugin](https://github.com/FlorianWoelki/obsidian-iconize) to leverage custom icon packs.



```md
<span data-icon="☢" class="ni t l" />

<span class="ni t l">Custom Text</p>

<span class="ni t r">:LiFolderTree:</p>

Your markdown here
```
