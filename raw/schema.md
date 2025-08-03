# Scotty Schema Language

Scotty Schema is a language for defining input/output validations for queries, their router, and the way data is loaded on the frontend.

## Packages

The project is split into several packages:

- [Parser](https://github.com/sayahoyahoy/scotty-schema/tree/main/packages/parser) - Parser for Scotty Schema language (parser, formatter, editor)
- [Compiler](https://github.com/sayahoyahoy/scotty-schema/tree/main/packages/compiler) - Compiler for code generation
- [Directives](https://github.com/sayahoyahoy/scotty-schema/tree/main/packages/directives) - Schema directives
- [Playground](https://github.com/sayahoyahoy/scotty-schema/tree/main/packages/playground) - Interactive testing environment

Scotty Schema is inspired by Prisma, with similar syntax, but is not compatible with it.

## Example Schema

```dart
type Customer extends person.Person omit registeredAt {
    id    ID
    email Email
    role  Role

    createdAt DateTime @default.now
}

routes {
    /// Get customer by id
    getItem(GET "/customers/:id") {
        params GetItemParams
        output Customer
    }
    upgradeCustomer(POST PUT "/customer/:id/upgrade/")
}

data customers {
    model = Customer

    getAllCustomers(CACHE pageable filterable) {
        output Customer[]
    }
}

operations {
    model = Customer
    regions = ["eu-central-1"]

    crud()
}

enum Role {
    USER  /// Default role
    ADMIN /// Administrator
}
```

## Table of Contents

- [Type Definitions](#type-definitions)
- [Field Types](#field-types)
- [Extending Types](#extending-types)
- [Directives](#directives)
- [Routes](#routes)
- [Data](#data-operations)
- [Operations](#internal-operations)
- [Enums](#enums)
- [Comments](#comments)

## Type Definitions

Types are defined using the `type` keyword.
A type represents a model or entity in your domain. It consists of fields that describe the properties of the type.
*Type Name* must start with a capital letter.

### Example

```dart
type User {
  id   ID
  name String
  age  Int?
  tags String[]
}
```

## Field Types

Fields in a type can be built-in types as well as user-defined types.

- `String`: Text value
- `Int`: 32-bit integer
- `Float`: Floating-point number
- `Boolean`: Logical value (true/false)
- `ID`: Unique identifier

Custom types can also be used as field types, referencing other type definitions within the schema.

### Nullable and List Types

- **Nullable Fields**: Use `?` after the type to make it optional
- **Lists**: Use `[]` to represent a list of a type. You can also use nested lists with multiple `[]`

### Examples

```dart
  name String?   // Optional text field
  tags String[]  // List of text values
```

## Extending Types

A type can extend an existing type and inherit its fields. Inherited fields can be modified using `omit` or `pick` modifiers.

### Extension Syntax

```dart
type Admin extends User
```

In this example, `Admin` will have all fields from the `User` type.

### Using Modifiers

- **Omit Modifier**: Used to exclude fields from the extended type.

  ```dart
  type Admin extends User omit password
  ```

  In this example, `Admin` inherits all fields from `User` except the `password` field.

- **Pick Modifier**: Used to include only specific fields from the extended type.

  ```dart
  type Admin extends User pick id | name
  ```

  In this example, `Admin` will only have `id` and `name` fields from `User`.

- **Namespaced Extends**: Types can extend types from other imports using a namespace.

  ```dart
  type LocalAdmin extends usr.User
  ```

  In this example, `LocalAdmin` extends the `User` type from the `usr` import.

## Directives

Directives are annotations that provide metadata or additional behavior to a type or field. They are prefixed by `@` and can be applied to types or individual fields.

### Example Directives

```dart
type User @entity {
  id   ID     @id @unique
  name String @computed
}
```

### Directive Arguments

Directives can take arguments. Arguments can be literals (e.g., strings, numbers), arrays, objects, or function calls.

- **Boolean Text Value**

  ```dart
  @dir(authorized)   // { authorized: true }
  ```

- **Unnamed Function Call**

  ```dart
  @dir(foo())   // { default: foo() } → unnamed argument will be assigned to 'default'
  ```

- **Named Parameters**

  ```dart
  @dir(foo: bar(), baz: "xy", qux: 3)   // { foo: bar(), baz: "xy", qux: 3 }
  ```

- **Combination of Named and Boolean Parameters**

  ```dart
  @dir(authorized, foo: bar(), flag: true)   // { authorized: true, foo: bar(), flag: true }
  ```

### Syntax
You can use single-line or multi-line notation.
Use a space or a comma as a separator.
```dart
@dir(authorized foo: bar())

@dir(
    foo: bar()
    baz: "xy"
    qux: 3
)
```

## Routes

Routes define the public API for Query. Routes are defined using the `routes` keyword.
Each route has an operation name, HTTP method, and path.

```dart
routes {
  updateUser(PUT "/users/:id") @auth.user {
    params UserParams
    input User
  }
}
```

### Route Methods

You can define multiple HTTP methods for a single route by separating them with a space.

```dart
updateUser(POST PUT "/users/:id")
```

Allowed HTTP methods are:
- `GET`
- `POST`
- `PUT`
- `DELETE`
- `PATCH`
- `OPTIONS`
- `ALL`

### Route Components

For each route, you can define the following components:
- `params`: URL path parameters
- `query`: query parameters
- `headers`: request headers
- `input`: input data
- `output`: output data

## Data Operations

Data operations define internal APIs used by the Scotty frontend. They are defined using the `data` keyword.
Each data operation can have caching strategy and additional features like pagination or filtering.

```dart
data customers {
    model = Customer

    getAllCustomers(CACHE pageable filterable) {
        output Customer[]
    }
}
```

### Data Operation Features

- **Caching Strategy**: Define how data should be cached (e.g., `CACHE`, `SYNC`)
- **Pagination**: Enable pagination with `pageable`
- **Filtering**: Enable filtering with `filterable`
- **Syncing**: Enable data syncing with `syncable`

### Data Operation Components

For each data operation, you can define the following components:
- `input`: input data
- `output`: output data

## Internal Operations

Internal operations define APIs that allow queries to call each other. They are defined using the `operations` keyword.
These operations are not exposed to the external API but can be used internally by other queries.

```dart
operations {
    model = Customer
    regions = ["eu-central-1"]

    crud()
}
```

### Operation Parameters

- **model**: The type that this operation applies to
- **regions**: List of regions where this operation is available

## Enums

Enums are defined using the `enum` keyword. Enums represent a set of named values.
Currently, only string values are supported.

### Example

```dart
enum Role {
  USER
  ADMIN
}
```

## Comments

Scotty Schema supports two types of comments:

- `// comment`: This type of comment is for readability and does not appear in the abstract syntax tree (AST) of the schema.
- `/// comment`: These comments are included in the AST as descriptions for AST nodes. Tools can use these comments to provide additional information. All comments are attached to the next available node; free-floating comments are not supported and are not included in the AST.

### Examples

```dart
/// This comment will be attached to the `User` node in the AST
type User {
  /// This comment will be attached to the `id` node in the AST
  id     ID     @default(autoincrement())
  // This comment is just for the reader
  weight Float  /// This comment will be attached to the `weight` node
}

// This comment is just for the reader and will not
// appear in the AST.

/// This comment will be attached to the
/// Customer node.
type Customer {}

/// This comment will be omitted from the AST as it is not attached to any node.
```
