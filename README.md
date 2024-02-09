# Obsidian Canvas Snippets

Here is a list of useful snippets to improve Obsidian Canvas.  
I will add more as I create them.  
Don't forget to share & star 🙂

# Node Icons
![image](https://github.com/ShahriarKh/obsidian-canvas-snippets/assets/31452340/e7bf311f-94fe-4725-829d-239b6ee1cd74)

## Snippet
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

## Usage
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

---

# Node Shapes

## Snippets
(The snippets are created for [Prism Theme](https://github.com/damiankorcz/Prism-Theme) and you probably need to tweak them, but the general idea is to use `clip-path` for the shape, and add some padding to the inner content.

### General

For centered-content style:
```css
.canvas-node:has(.shape-rhombus, .shape-hexagon, .shape-circle) {
  .markdown-rendered {
    &::before {
      display: none !important;
    }

    &::after {
      display: none !important;
    }
  }
}

.canvas-node:has(.node-center) {
  .markdown-rendered .markdown-preview-section {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    height: 100%;

    > div * {
      text-align: center !important;
      text-align-last: center !important;
    }
  }
}
```


### Circle

<img src="https://github.com/ShahriarKh/obsidian-canvas-snippets/assets/31452340/42a77ceb-f8d3-4e00-8e1e-b2d676c46a9b" height="400px" />

```css
.canvas-node:has(.shape-circle) {
  &.is-focused {
    background-color: rgba(0, 0, 0, 0.5);
  }

  .canvas-node-container {
    border-radius: 50%;
    aspect-ratio: 1 / 1;
    height: 100%;
    width: auto;

    .markdown-embed-content {
      padding: 15%;
    }

    .markdown-rendered {
      padding: 0 !important;

      &::before {
        display: none;
      }

      &::after {
        display: none;
      }
    }
  }
}
```

### Rhombus

<img src="https://github.com/ShahriarKh/obsidian-canvas-snippets/assets/31452340/02d14551-fe2c-4655-9757-c95609514514" height="400px" />

```css
.canvas-node:has(.shape-rhombus) {
  border: solid 4px hsl(var(--canvas-color)) !important;
  background: hsl(var(--canvas-color)) !important;
  clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);

  .canvas-node-container {
    clip-path: inherit;
    border: none !important;

    .markdown-embed-content {
      padding: calc(var(--canvas-node-height) / 4)
        calc(var(--canvas-node-width) / 4);
    }

    .markdown-rendered {
      padding: 8px !important;
    }
  }
}
```

### Hexagon

<img src="https://github.com/ShahriarKh/obsidian-canvas-snippets/assets/31452340/695319ba-995c-4259-a371-88b38bc1c387" height="400px" />

```css
.canvas-node:has(.shape-hexagon) {
  border: solid 2px hsl(var(--canvas-color)) !important;
  background: hsl(var(--canvas-color)) !important;
  clip-path: polygon(25% 0%, 75% 0%, 100% 50%, 75% 100%, 25% 100%, 0% 50%);
  /* for regular hexagon */
  aspect-ratio: 8 / 7;
  width: auto !important;

  .canvas-node-container {
    clip-path: inherit;
    border: none !important;
  }

  .markdown-embed-content {
    padding: 16% 16%;
  }

  .markdown-rendered {
    padding: 8px !important;
  }
}
```
