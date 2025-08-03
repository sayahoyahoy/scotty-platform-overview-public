# AutoForm :sparkles:

A form component that renders based on Scotty model schema. Instead of defining data structure, users only need to specify how individual fields should be rendered. AutoForm handles all data updates in the model, ensuring deep value updates without affecting other data.

## Contents

- [Basic Usage](#basic-usage-rocket)
- [Field Mapping](#field-mapping-world_map)
- [Arrays](#arrays-books)
- [Parameters (key/value arrays)](#parameters-key)
- [Custom Form Layout](#custom-form-layout-art)
- [Reusable Form](#reusable-form-recycle)
- [Multiple AutoForms for a Single Model](#multiple-autoforms-for-a-single-model-arrows_counterclockwise)
- [Dynamically Adapting the Form Based on Its Own State](#dynamically-adapting-the-form-based-on-its-own-state-brain)
- [Default Rendering (Dev Mode)](#default-rendering-dev-mode-hammer_and_wrench)

AutoForm also provides field controls and allows custom templates for:

* Individual fields
* Arrays
* Array items
* Objects

The `model` must be a Scotty model returned from `useData()`. This provides AutoForm with both the schema (used to render the form structure) and the reactive data (used for updates, defaults, and validation).

## Basic Usage :rocket:

### Scotty Language
```pug
const modelData = useData('queries', {id: 123})

AutoForm(
    model="modelData"
    fields="{ myField: {type: 'number'} }"
    path="$.whatever.deep.[].path"
)
    +myField({value, update})
        input(type="number" :value="value" @input="update($event.target.value)")
```

### Equivalent in pure Vue.js

```vue
<AutoForm
    :model="modelData"
    :fields="{ myField: {type: 'number'} }"
    path="$.whatever.deep.[].path"
>
    <template #myField="{ value, update }">
        <input type="number" :value="value" @input="update($event.target.value)" />
    </template>
</AutoForm>
```

## Field Mapping :world_map:

### Type Mapping

```js
{myBool: {
    type: 'boolean'
}}
```

### Path Mapping

AutoForm uses an extended JSON Path syntax:

* `[]` targets array items content
* `[$]` specifically targets array item wrappers for array-specific actions (move, delete)

Example:

```js
{myField: {
    path: '$.steps.[].name'
}}
```

## Arrays :books:

The form renders arrays in this structure:

```
$.myArray          <- array wrapper
$.myArray.[$]      <- array item wrapper
$.myArray.[]       <- array item content (object or direct field)
$.myArray.[].name  <- field inside object
```

The array wrapper provides `addItem` and `addItemFirst` methods to create items with default values from schema.

The array item wrapper provides `moveUp`, `moveDown`, and `remove` methods.

To enable automatic rendering continuation, use the `AutoFormYield` component inside the *wrapper*. `AutoFormYield` acts as a placeholder for rendering child fields or components.

### Example

```js
const fields = ref({
    myArray: {path: '$.steps'},
    myArrayItem: {path: '$.steps.[$]'},
})
```

```pug
AutoForm(
    :model="modelData"
    :fields="fields"
)
    +myArray({addItem})
        div.myArray
            AutoFormYield
            button(@click="addItem") Add Item

    +myArrayItem({removeItem})
        div.myArrayItem
            button(@click="removeItem") ×
            AutoFormYield
```

## Parameters :key:

Managing key-value object fields in array can be challenging. AutoForm provides a component (`AutoFormParameters`) that converts arrays into object-like structures, handling data updates in the original array.

Props:

* `fields`: Specify which fields to render.
* `sort`: Specify sorting order of fields.
* `hide`: Fields listed here are hidden from rendering, but still included in the data.

The Parameters component accepts templates for individual fields.

### Example

```pug
AutoForm(
    :model="modelData"
    fields="{ myParams: {path: '$.steps.[].parameters'} }"
)
    +myParams
        AutoFormParameters(
            fields="['collection', 'command', 'function']"
        )
            +command({value, update})
                button(@click="update('A')") option A
                button(@click="update('B')") option B
```

## Custom Form Layout :art:

AutoForm by default renders fields in a column layout. However, if you need a custom layout, you can use the default slot and the `AutoFormYield` component to render individual fields at any place in the structure. Slots for specific fields remain available. You can combine the default slot and the AutoFormYield component to create complex layouts while preserving AutoForm's reactivity and field logic.

### Example

```pug
AutoForm(
    :model="modelData"
    :fields="{ myArray: {path: '$.steps'} }"
)
    div.myForm
        div.colLeft
            AutoFormYield(path="$.steps")
        div.colRight
            AutoFormYield(path="$.collection")
            AutoFormYield(path="$.data")

    +myArray
        label My Array
        AutoFormYield
```

## Reusable Form :recycle:

You can encapsulate common field layouts into reusable form components. This helps maintain consistent UX and reduce boilerplate.

### Custom Form Wrapper (Reusable Style)

```pug
const model = props.model
const fields = computed(() => ({
    text: {type: 'string'},
    number: {type: 'int'},
    ...props.fields,
}))

AutoForm(
    :model="model"
    :fields="fields"
)
    +text({value, update})
        input(type="text" :value="value" @input="update($event.target.value)")

    +number({value, update})
        input(type="number" :value="value" @input="update($event.target.value)")

    slot
```

### Example of Reuse

```pug
MyCustomForm(
    :model="modelData"
    :fields="{myField: {path: '$.steps.[].name'}}"
)
    +myField({value, update})
        div {{ value }}
        button(@click="update(value + 1)") Add
```

## Multiple AutoForms for a Single Model :arrows_counterclockwise:

If you need to render different parts of the form conditionally or across separate UI sections, you can use multiple AutoForm components with the same model instance.

Each AutoForm always accepts the full model (not a nested part), and you control which part of the schema to render using the `path` prop. It doesn't matter how many AutoForms are accessing the same model – the model is a singleton (or a forked instance), and changes are always synchronized.

```vue
AutoForm(:model="modelData" :path="$.steps")
div.differentPart
    AutoForm(:model="modelData" :path="$.params")
```

This makes it easy to build dynamic layouts, progressive forms, and reusable partial forms while keeping everything connected to a single source of truth.

## Dynamically Adapting the Form Based on Its Own State :brain:

You can build self-adaptive forms by reacting to changes in the model and adjusting which fields should be shown or rendered differently.

```js
const modelData = useData('queries', {id: 123})

const methods = ref(['getItem', 'updateItem', 'crud'])

const selectedCommand = computed(() => {
    return modelData.value?.steps[0].parameters.find(p => p.name === 'command')?.value
})

const paramsNames = computed(() => {
    switch (selectedCommand.value) {
        case 'getItem':
            return ['a', 'b', 'c', 'command']
        case 'updateItem':
            return ['b', 'c', 'command']
        case 'crud':
            return ['a', 'b', 'c', 'd', 'e', 'f', 'command']
        default:
            return ['command']
    }
})
```
```pug
AutoForm(
    :model="modelData"
    :path="$.steps.0.parameters"
    :fields="{myParams: {path: '$.steps.[].parameters'}}"
)
    +myParams
        AutoFormParameters(
            fields="selectedParams"
            sort="['command']"
        )
            #command({ value, update })
                select(
                    :value="value"
                    @change="update($event.target.value)"
                )
                    option(
                        v-for="method in methods"
                        :key="method"
                    ) {{ method }}
```

In this example, the form reads its own state (`command`) and updates the rendered parameters accordingly.
`sort` ensures `command` appears first, and because a custom template is provided, AutoForm automatically skips rendering it in the default output.

## Default Rendering (Dev Mode) :hammer_and_wrench:

If you provide only the model prop and nothing else, AutoForm renders a full, unstyled form based on the schema.

This is ideal for debugging or development workflows:

```pug
AutoForm(:model="modelData")
```

* All fields from the schema are rendered
* No layout or styles are applied
* Field paths are shown to help with debugging
* Useful for quickly testing models or discovering structure

To use custom layout and design, create a reusable FormComponent and override field templates.
