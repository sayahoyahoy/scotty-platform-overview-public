# Scotty Template Editor

The `TemplateEditor` class is designed for AI agents to manipulate Scotty Template code. It provides programmatic template editing through a simple API.

## Constructor

Creates a new editor instance with an existing template.

```typescript
const editor = new TemplateEditor(`
user-card.my-user-card
    h3 {{ user.name }}
    p.title {{ user.title }}
`)
```

## create(template: string)

Reinitializes the editor with a new template.

```typescript
editor.create(`
nav.main-nav
    a(href="/home") Home
    a(href="/about") About
`)
```

## addElement(template: string, targetSelector: string, position?: 'inside' | 'before' | 'after')

Adds a new element to the existing template.

**Adding inside:**
```typescript
editor.addElement('button[variant="primary"] Save', '.actions')
```

Result:
```pug
// before
div.actions

// after
div.actions
    button[variant="primary"] Save
```

**Adding before element:**
```typescript
editor.addElement('h2 Welcome', '.content', 'before')
```

Result:
```pug
// before
div.content
    p Existing content

// after
h2 Welcome
div.content
    p Existing content
```

**Adding after element:**
```typescript
editor.addElement('footer Copyright 2024', '.main', 'after')
```

Result:
```pug
// before
div.main
    p Main content

// after
div.main
    p Main content
footer Copyright 2024
```

## moveElement(sourceSelector: string, targetSelector: string, position?: 'inside' | 'before' | 'after')

Moves an existing element to a new location.

```typescript
editor.moveElement('.sidebar', '.main-content', 'after')
```

Result:
```pug
// before
div.sidebar Sidebar content
div.main-content
    p Main content

// after
div.main-content
    p Main content
div.sidebar Sidebar content
```

## removeElement(selector: string)

Removes element from the template.

```typescript
editor.removeElement('.deprecated-section')
```

Result:
```pug
// before
div.container
    div.content Important content
    div.deprecated-section Old content
    div.footer Footer

// after
div.container
    div.content Important content
    div.footer Footer
```

## renameClass(selector: string, oldClassName: string, newClassName: string)

Renames CSS class on selected elements.

```typescript
editor.renameClass('div.container', 'old-style', 'new-style')
```

Result:
```pug
// before
div.old-style.container
    p Content

// after
div.new-style.container
    p Content
```

## removeClass(selector: string, className: string)

Removes CSS class from selected elements.

```typescript
editor.removeClass('button', 'disabled')
```

Result:
```pug
// before
button.primary.disabled Save
button.secondary.active Cancel

// after
button.primary Save
button.secondary.active Cancel
```

## replaceElement(selector: string, newElementTemplate: string)

Replaces existing element with a new element defined in Scotty Template syntax.

```typescript
editor.replaceElement('.old-button', `
default-button[variant="secondary"](@click="handleClick") New Action
`)
```

Result:
```pug
// before
div.actions
    button.old-button Click me
    a(href="/cancel") Cancel

// after
div.actions
    default-button[variant="secondary"](@click="handleClick") New Action
    a(href="/cancel") Cancel
```

## getTemplate()

Returns the resulting template in Scotty Template syntax.

```typescript
const result = editor.getTemplate()
console.log(result)
```

Output:
```pug
user-card.my-user-card
    h3 {{ user.name }}
    default-button[variant="primary"] Contact
```

## Complete Workflow Example

```typescript
const editor = new TemplateEditor(`
article.blog-post
    h1 {{ post.title }}
    p.meta By {{ post.author }}
`)

editor
    .addElement('div.tags', 'article', 'inside')
    .addElement('span.tag {{ tag }}', '.tags')
    .addElement(`
        div.actions
            button[variant="primary"](@click="share") Share
            button[variant="secondary"](@click="save") Save
    `, 'article')
    .renameClass('article', 'blog-post', 'post-card')

const finalTemplate = editor.getTemplate()
```

Final template:
```pug
article.post-card
    h1 {{ post.title }}
    p.meta By {{ post.author }}
    div.tags
        span.tag {{ tag }}
    div.actions
        button[variant="primary"](@click="share") Share
        button[variant="secondary"](@click="save") Save
```