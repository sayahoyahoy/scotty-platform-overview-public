# Scotty Template Syntax

Scotty template syntax is inspired by Pug and offers a concise, readable way to write templates.
Unlike HTML, there are no closing tags—structure is determined by indentation.

Scotty Template compiles into Vue, which means it supports all Vue ecosystem features and functionality. Thanks to this integration, you can leverage Vue's reactivity, components, directives, slots, and other features directly within Scotty Template syntax, but with a more elegant and concise notation.

## Documentation

- **[Template Syntax](README.md)** - This document - learn the Scotty Template syntax
- **[API Reference](README-API.md)** - Programmatic API for parsing and compiling templates
- **[Template Editor](README-editor.md)** - AI-friendly API for manipulating template code

### Usage Example

```pug
user-card.my-user-card[compact]
    +avatar
        if user.avatar
            img(:src="user.avatar" :alt="user.name")
        else
            div.avatar-placeholder {{ user.initials }}

    +user-info
        h3 {{ user.name }}
        p.title {{ user.title }}

    +action
        default-button[variant="primary"](@click="...") Contact
        default-button[variant="secondary" :disabled="!canFollow"](@click="...") Follow
```

## Basic Elements

### Classes & IDs

```pug
// Element with a class
div.container

// Element with multiple classes
div.container.fluid

// Element with an ID
div#main-content

// Combination of classes and ID
div#main-content.container.fluid
```

### Attributes (Props)

```pug
// Element with attributes
my-component(type="primary" placeholder="Your name")

// Attributes can be multiline
my-component(
    type="secondary"
    class="wide"
    disabled
)

// JavaScript values (use ":" prefix)
my-component(:value="user.name" :disabled="!isEditable")

// Multiline attribute value
my-component(
    description=`This is
    a multiline
    value`
)
```

### Events

You can attach Vue-style event listeners to components using the `@` syntax:

```pug
// Basic event handling
my-component(@click="handleClick")

// Event with modifier
button(@click.stop="stopPropagation")

// Multiple modifiers
form(@submit.prevent.once="submitForm")

// Keyboard events with key modifiers
input(@keyup.enter="search")
```

#### Available Event Modifiers

- `.stop` - calls `event.stopPropagation()`
- `.prevent` - calls `event.preventDefault()`
- `.capture` - uses event capturing instead of bubbling
- `.self` - only trigger if event target is the element itself
- `.once` - trigger the handler at most once
- `.passive` - improves scrolling performance with `{ passive: true }`

#### Key Modifiers

- `.enter`, `.tab`, `.delete`, `.esc`, `.space`, `.up`, `.down`, `.left`, `.right` - specific keys
- `.ctrl`, `.alt`, `.shift`, `.meta` - modifier keys
- `.exact` - control exact combination of system modifiers

#### Mouse Modifiers

- `.left`, `.right`, `.middle` - specific mouse buttons

### Variants

Variants allow you to specify different component styles.

```pug
// Variant with a string value
my-component[variant="primary"]

// Multiple variants
icon[size="large" color="red"]

// Variant with a JavaScript expression
my-component[:is-active="isActive"]
my-component[:data-count="items.length"]

// Boolean variant (flag present = true)
my-component[selected]

// Combination of all types
my-component[
    variant="outline"
    loading
    :selected="isSelected"
]
```

---

## Text Content

```pug
// Text on the same line as the element
p This is a simple paragraph

// Verbatim text content with "|" prefix
my-component
    | This is verbatim text
    | preserved exactly as written,
    | including
    | newlines.
```

---

## Logic Blocks

### Conditionals

```pug
// Simple if
if user.isLoggedIn
    p Welcome, {{ user.name }}!

// if-else
if user.isLoggedIn
    p Welcome back!
else
    a(href="/login") Log in

// if-elseif-else
if user.isAdmin
    p You have admin rights
elseif user.isPremium
    p You have a premium account
else
    p You have a standard account
```

### Switches

```pug
switch user.role
    case "admin"
        p Administrator
    case "moderator"
        p Moderator
    default
        p Regular user
```

### Pattern Matching

```pug
match data
    with {type: "success", message}
        my-component.success {{ message }}
    with {type: "error", message}
        my-component.error {{ message }}
    else
        my-component.alert Unknown status
```

### Loops

```pug
// Iterate over an array
for item in items :key="item.id"
    my-component {{ item.name }}

// With index
for item, index in items :key="item.id"
    my-component {{ index + 1 }}. {{ item.name }}
```

---

## Slots

Slots allow you to insert content into component slots.

```pug
// Using a component with slots
my-dialog
    +header
        h2 Dialog title

    +content({client})
        p client name: {{client.name}}

    +footer
        button Close
```

---

## Comments

```pug
// This is a comment (will not appear in output)

/// This is a documentation comment

my-component(
    foo="bar" // This is a trail comment
    baz="xyz" /// This is a documentation trail comment
)
```
