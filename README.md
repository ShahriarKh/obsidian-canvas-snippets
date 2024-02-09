# Obsidian Canvas Snippets

Here is a list of useful snippets to improve Obsidian Canvas.  
I will add more as I create them.  
Don't forget to share & star 🙂

(The snippets are created for [Prism Theme](https://github.com/damiankorcz/Prism-Theme) and you probably need to tweak them)

Contents:
- [Node Icons](#node-icons)
- [Node Shapes](#node-shapes)

# Node Icons
![image](https://github.com/ShahriarKh/obsidian-canvas-snippets/assets/31452340/e7bf311f-94fe-4725-829d-239b6ee1cd74)

## ✍🏽 Usage
First add the snippets, then place one or more spans in your node, including the `ni` class (short for "node icon"), icon position, and the icon itself.

- Positions:
  - Horizontal: `l` (left), `c` (center), `r` (right)
  - Vertical: `t` (top), `m` (middle), `b` (bottom)
- Icon Types:
  - Emoji: `<span data-icon="🎈"></span>`
  - Text: `<span>Custom Text</span>`
  - Custom Icon (using [Iconize Plugin](https://github.com/FlorianWoelki/obsidian-iconize)): `<span>:LiFolderTree:</span>`

Here are three examples:
```md
Your markdown here

/* emoji as icon, top left */
<span data-icon="☢" class="ni t l" />

/* text as icon, bottom left */
<span class="ni b l">Custom Text</span>

/* text as icon, middle right */
<span class="ni m r">:LiFolderTree:</span>

Your markdown here
```

> [!NOTE]
>  Middle `m` and center `c` positions don't work correctly with custom shapes, because of `overflow`.

## 📃 Snippet
Add this css snippet. Feel free to change padding, margin and others based on your theme styles.
```css
.canvas-node:not(.is-editing) {
  transform: rotate(0deg);

  .ni {
    padding: 4px;
    position: absolute;
    color: hsl(var(--canvas-color));
    height: max-content;

    &[data-icon] {
      padding: 0;
      font-family: "Segoe UI Emoji";
      font-size: 1rem;

      &:before {
        content: attr(data-icon);
      }
    }

    &.t {
      top: 0;
    }

    &.m {
      top: calc(50% - 12px);
    }

    &.b {
      bottom: 0;
    }

    &.r {
      right: -12px;
    }

    &.c {
      left: calc(50% - 4px);
    }

    &.l {
      left: 0;
    }
  }
}
```


---

# Node Shapes

## ✍🏽 Usage
After adding the snippets, you can add any element (like a `<span>`) including the class name of the shape. For example, to create a circular node with centered content, put this in your node:

```md
Your node content...

<span class="shape-circle node-center"></span>
```

## 📃 Snippets

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

## 💎 Creating Shapes
In oreder to create your custom shape, you can use this template:
```css
.canvas-node:has(.shape-your-shape-name) {
  border: solid 2px hsl(var(--canvas-color)) !important;
  background: hsl(var(--canvas-color)) !important;

  clip-path: /* shape path */

  .canvas-node-container {
    clip-path: inherit;
    border: none !important;
  }

  .markdown-embed-content {
    padding: /* padding 1 */
  }

  .markdown-rendered {
    padding: /* padding 2 */
  }
}
```
Replace `clip-path` value with your desired shape path, and change the paddings to make the inner content look readable.
[Clippy](https://bennettfeely.com/clippy/) is a great tool for working with css paths.

Here's a simple example, using Obsidian logo as a custom shape!

<div style="display:flex;flex-direction:row;justify-content:center;gap:12px">
  <img src="https://github.com/ShahriarKh/obsidian-canvas-snippets/assets/31452340/ba185f84-6584-4e12-8269-7edb496b764a" height="300px"/>
  <img src="https://github.com/ShahriarKh/obsidian-canvas-snippets/assets/31452340/7965889f-f3ed-4464-9628-e6507b8996e8" height="300px" />
</div>


