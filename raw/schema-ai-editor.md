# EditorAI

EditorAI is a wrapper around Editor and AstBuilder that simplifies working with text schema definitions in Scotty Schema format. It automatically uses AstBuilder to parse text inputs and then uses Editor to apply changes to the AST document.

## Usage

```typescript
import {EditorAI} from './editor-ai'
import {Document} from './scotty-schema-ast'

// Create an empty document
const document: Document = {
    kind: 'Document',
    definitions: [],
}

const editorAI = new EditorAI(document)

editorAI.addTypeDefinition(`
  type User {
    id ID @id
    name String
    email String @unique
  }
`)

editorAI.addFieldToType('User', 'createdAt DateTime @default(now())')

editorAI.addFieldToType('User', 'updatedAt DateTime', {before: 'createdAt'})

editorAI.removeFieldFromType('User', 'email')

editorAI.addEnumDefinition(`
  enum Role {
    ADMIN
    USER
  }
`)
editorAI.addValueToEnum('Role', 'MANAGER', {after: 'ADMIN'})

const updatedDocument = editorAI.getDocument()

const formatter = new Formatter({
    indentationSize: 4,
    sortTypes: false,
    sortFields: false,
    alignFields: true,
})

const updatedSchema = formatter.format(updatedDocument)

/*
type User {
    id        ID @id
    name      String
    updatedAt DateTime
    createdAt DateTime @default(now())
}

enum Role {
    ADMIN
    MANAGER
    USER
}
*/
```

## Available Methods

### Types

- `addTypeDefinition(schema: string, afterDefinition?: string)`: Adds a type definition from a string representation
- `addFieldToType(typeName: string, fieldSchema: string, position?: Position)`: Adds a field to an existing type
- `removeFieldFromType(typeName: string, fieldName: string)`: Removes a field from an existing type

### Enums

- `addEnumDefinition(schema: string, afterDefinition?: string)`: Adds an enum definition from a string representation
- `addValueToEnum(enumName: string, valueSchema: string, position?: Position)`: Adds a value to an existing enum
- `removeValueFromEnum(enumName: string, valueName: string)`: Removes a value from an existing enum

### Routes

- `addRoutesDefinition(schema: string, afterDefinition?: string)`: Adds a routes definition from a string representation
- `addRoute(routeSchema: string, position?: Position)`: Adds a route to an existing routes definition
- `removeRoute(operationName: string)`: Removes a route by operation name

### Data

- `addDataDefinition(schema: string, afterDefinition?: string)`: Adds a data definition from a string representation
- `addDataOperation(dataName: string, operationSchema: string, position?: Position)`: Adds an operation to an existing data definition
- `removeDataOperation(dataName: string, operationName: string)`: Removes an operation from an existing data definition
- `addDataParameter(dataName: string, paramSchema: string, position?: Position)`: Adds a parameter to an existing data definition
- `removeDataParameter(dataName: string, paramName: string)`: Removes a parameter from an existing data definition

### Operations

- `addOperationsDefinition(schema: string, afterDefinition?: string)`: Adds an operations definition from a string representation
- `addOperation(operationSchema: string, position?: Position)`: Adds an operation to an existing operations definition
- `removeOperation(operationName: string)`: Removes an operation from an existing operations definition
- `addOperationsParameter(paramSchema: string, position?: Position)`: Adds a parameter to an existing operations definition
- `removeOperationsParameter(paramName: string)`: Removes a parameter from an existing operations definition

### General

- `removeDefinition(name: string)`: Removes a definition by name
- `getDocument()`: Returns the current document

## Position Interface

Most methods support a `position` parameter that allows you to specify where to insert new items. This is a `Position` object with the following properties:
- `before?: string` - Insert the item before the specified item
- `after?: string` - Insert the item after the specified item

If no position is specified, items are added to the end of the respective list.

Example usage:
```typescript
// Add a field at the end of fields list
editorAI.addFieldToType('User', 'createdAt DateTime')

// Add a field after another field
editorAI.addFieldToType('User', 'updatedAt DateTime', {after: 'createdAt'})

// Add a field before another field
editorAI.addFieldToType('User', 'id ID', {before: 'name'})
```

## Example of Complex Schema Editing

```typescript
// Build an entire schema step by step
editorAI.addTypeDefinition(`
  type User {
    id ID @id
  }
`)

editorAI.addFieldToType('User', 'name String @required')
editorAI.addFieldToType('User', 'email String @unique', {after: 'name'})

editorAI.addEnumDefinition(`
  enum Role {
    ADMIN
  }
`)

editorAI.addValueToEnum('Role', 'USER')
editorAI.addValueToEnum('Role', 'MANAGER', {after: 'USER'})

editorAI.addDataDefinition(`
  data users {
    model = User
  }
`)

editorAI.addDataOperation('users', 'list(CACHE pageable)', {after: 'list'})
editorAI.addDataOperation('users', 'get(NO_CACHE)')

editorAI.addRoutesDefinition(`
  routes {
  }
`)

editorAI.addRoute('getUsers(GET "/users") @auth.user')
editorAI.addRoute('createUser(POST "/users") @auth.admin', {after: 'getUsers'})
```