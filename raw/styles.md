# Scotty Style Syntax

In Scotty, styles are written using a minimal, indentation-based syntax. Each component is assigned a **semantic class**—one clear class name used in the template. This class is then used in styles to define or override its appearance. Inside the style block, you can mix:

- Regular CSS declarations (`color red`)
- Tailwind utility classes (`text-sm px-4`)
- Nested rules (`&:hover`, `> .icon`)
- Variants (`&:selected`, `&:variant(primary)`)
- Deep selectors (`.myCmp::footer::okButton`)

Scotty will automatically **group and sort Tailwind utilities**, so you can write them inline and let the formatter clean it up.

---

## Example

### Template

```pug
my-button.myButton[selected]
````

### Style

To make component styles extendable, the root element of the component must have the `.root` class.

```stylus
.root

.myButton
    bg-white text-gray-800
    px-4 py-2 text-sm font-bold
    border border-gray-300 rounded-md
    hover:bg-gray-100
    transition duration-200
```

Sorted output:

```stylus
.myButton
    /* layout */
    px-4 py-2
    /* spacing */
    /* appearance */
    text-sm font-bold bg-white text-gray-800 border border-gray-300 rounded-md hover:bg-gray-100
    /* behavior */
    transition duration-200
```

---

## Nesting

Nested selectors follow CSS logic, but indentation defines structure. Always use 4-space indentation.

```stylus
.myButton
    bg-blue-600 text-white

    &:hover
        bg-blue-700

    &:selected
        bg-green-600

    &:variant(primary)
        bg-blue-600 text-white

    &:variant(secondary)
        bg-gray-200 text-gray-900

    > .icon
        mr-2 text-lg
```

---

## Deep part styling

When a component exposes internal parts using `::`, you can target them directly:

```stylus
.myDialog::footer::okButton
    font-bold
    hover:text-blue-400
```

---

## Overriding component CSS variables

Scoped variables can be defined in components and overridden where used.

### In component:

```stylus
.root
    --accent-color #f87171

.body
    background var(--accent-color)
```

### When used:

```stylus
.mySelect
    --accent-color #60a5fa
```

---

## Enum variant styling

For components using enum variants:

### Style

```stylus
.myAlert
    &:variant(success)
        border-green-500 text-green-800

    &:variant(error)
        border-red-500 text-red-800
```

### Template

```pug
my-alert.myAlert[variant="success"]
```

---

## Notes

* One semantic class per part of compoent (.root, .body, .item, .card)
* Tailwind utilities are grouped automatically: layout, spacing, appearance, behavior
* Use `&:` prefix for pseudo-classes or variants
* Use `::` for targeting parts inside other components
* Variables use native `--var` syntax and follow CSS scoping rules