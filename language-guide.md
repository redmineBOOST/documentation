---
layout: documentation
title: Language Guide
id: language_guide
---
# <a name="languageGuide"></a> Language Guide

The **redmineBOOST** Language v1.0 (RBO) is specially designed to describe Redmine tasks. RBO is highly declarative in a way that each task can be described as an item. An item has properties which can be accessed and if it is not readonly it can be modified. To get the necessary data from Redmine there are queries which can be stored into fields or directly passed into properties.

The main design goals of the language are readability, error reduction and intuitive handling of compactness.

## Notation
The documentation will use the following notations:

> This is an important statement.

Important attributes are shown in **bold** or *italics*.

The syntax is partially explained by a kind of Backus–Naur Form (BNF) with the following meanings:

`(...)`: A group of elements.

`(...)?`: An optional group of elements.

`*`: Repeat from 0 to n times.

`+`: Repeat from 1 to n times.

`<abc>`: A placeholder with the name abc.

## <a name="itemInstantiations"></a> Item Instantiations

Item Instantiations are the core element of a process description. They represent the tasks which should be executed. They are executed in declaration order (top-down).

The format of an item instantiation is defined as follows:

`<predefinedTypeSpecifier> { (<propertyDefinition> | <itemInstantiation> | <fieldDeclaration>)* }`

The Item scope `<predefinedTypeSpecifier> {...}` can contain multiple [Property Definitions](#propertyDefinitions), [Item Instantiations](#itemInstantiations) and [Local Field Declarations](#localFieldDeclarations).

The instantiable Items can be defined as follows:
```
let issue1: Issue = Issue {
    project: GetProject(identifier="project1")
    subject: "Example Subject"
    tracker: GetTracker(name="tracker1")

    Issue {
        project: GetProject(identifier="project1")
        subject: "Example Subject"
        tracker: GetTracker(name="tracker1")
    }
}
```

In the example the Issue with the *identifier* `issue1` was defined with all required properties (`project`, `subject` and `tracker`). Furthermore it contains a top-level nested Issue. This nesting automatically results in setting the parent property of the nested Issue to `issue1`. As a result Redmine would create an Issue containing a Child-Issue.

Top-level Item Instantiations result in structural child items, otherwise the items are treated as independent.

Example:
```
let issue1: Issue = Issue {
    project: GetProject(identifier="project1")
    subject: "Example Subject"
    tracker: GetTracker(name="tracker1")

    let issue2Subject: Issue = Issue {
        project: GetProject(identifier="project1")
        subject: "Example Subject"
        tracker: GetTracker(name="tracker1")
    }.subject
}
```

In this example, the nested issue is treated as a standalone issue because its `subject` property is accessed immediately. Therefore, it is not a child Issue of `issue1`.

### <a name="propertyDefinitions"></a> Property Definitions

Property Definitions set specific attributes of the containing [Item Instantiation](#itemInstantiations).

> Each property is beginning with a lowercase letter.

The format of a property definition is defined as follows:

`<identifier>: <expression>? (Newline | ;)`

`identifier`: Identifier used to reference the property in the [Item](#item).

`expression`: The property assignment expression can be assigned with Literals, Enumerations constants, Items and Query invocation results.

`Newline | ;`: Each property definition must end with a line break or a semicolon.

### <a name="localFieldDeclarations"></a> Local Field Declarations

Fields can be assigned with Literals, Enumerations constants, Items and Query invocation results.

A local field declaration is initialized immediately when the containing Item is declared.

> Fields have the type specified so the assigning type has to match the defined field type.

Field identifiers must begin with a lowercase letter.

The `let` keyword changes the visibility of the field for the area that contains it, while the `global` keyword sets the visibility of the field to the global area.
Therefore it is accessible from everywhere.

Fields are declared as follows:

`(let | global) <identifier>: <typeSpecifier> = <expression> (Newline | ;)`

`identifier`: Identifier used to reference the field.

> Identifiers must begin with `a-z`, `A-Z` or `_` followed by `0-9`, `a-z`, `A-Z` or `_`.

`typeSpecifier`: The data type of the field.

`expression`: The field assignment expression can be assigned with Literals, Enumerations constants, Items, Item Instantiations and Query invocation results.

`Newline | ;`: Each field declaration must end with a line break or a semicolon.

Example:
```
Issue {
    let subjectText: string = "Example Subject"

    project: GetProject(identifier="project1")
    subject: subjectText
    tracker: GetTracker(name="tracker1")
}
```

In the example the field with the name `subjectText` has the type [string](#string) and is assigned to the string literal `"Example Subject"`.

## <a name="globalFieldDeclarations"></a> Global Field Declarations

Global Fields behave exactly as local field declarations except that they are defined at the global scope and are not contained in an [Item Instantiation](#itemInstantiations).

A global field declaration is initialized immediately.

Example:
```
let currentUser: User = GetCurrentUser()
```

In the example the field with the name `currentUser` has the type User and is assigned to the result of the query invocation of `GetCurrentUser()`.
The keyword `global` is unnecessary in this case, because global fields are already defined in the global scope. Therefore, they are already accessible from anywhere.

## <a name="scopes"></a> Scopes

In general a Scope is a concept that refers to where values of [properties](#propertyDefinitions) and [fields](#localFieldDeclarations) can be accessed.

There are basically two scope types:
* *Global scope*  (a value in the global scope can be used anywhere in the entire process)
* *Item block scope* (only visible within a `{ ... }` codeblock)

Each [property](#propertyDefinitions) and [field](#localFieldDeclarations) is visible in all inner scopes. When the user refers to a property, the property is searched from the referenced location upwards in all scopes and the first property matching the name is chosen.

Example:
```
let subjectText: string = "Example Subject"
Issue {
    project: GetProject(identifier="project1")
    subject: subjectText
    tracker: GetTracker(name="tracker1")

    Note {
        // Reference the subject of the issue
        text: subject
    }
}
```
In the example the Issue was defined with all required properties (`project`, `subject` and `tracker`). Furthermore it contains a Sub-Item Note which references the `subject` of `issue1` and assigns it to the `text` property of the Note. The scope of the Note has no other property or field named `subject`, so it is searched for in the parent scope and found there. The `subject` of the issue is set to the field `subjectText` located in the global scope. As a result Redmine would create an Issue with a Note which contains the subject of the Issue as text.

## <a name="queries"></a> Queries

Queries are basically getters for Redmine data. Each time someone wants to access access an existing element of Redmine they have to use a Query.

> The parameters of a query must always be named explicitly.

All properties of the object returned by the query are `readonly`.
To change data of the item returned by the query, one should use the special update item.

Queries are defined as follows:

`<identifier> ( (<argumentIdentifier>=<expression>)? (,<argumentIdentifier>=<expression>)* )`

`identifier`: Identifier of the query.

`argumentIdentifier`: Identifier of the query argument.

`expression`: The query argument expression can be assigned with Literals, Enumerations constants, Items and Query invocation results.

Queriess can be used as follows:
```
GetUser(id=1)
GetUser(login="mmustermann")
```

In the example the query `GetUser` is called one time with the parameter `id` set to `1` and another time with the parameter `login` set to `mmustermann`.
Each Query in the example returns a [User](#user). If the [User](#user) is not found or another error occurred a diagnostic will be shown.

## <a name="itemTracking"></a> Item Tracking

**redmineBOOST** automatically tracks Redmine Items.
This means that Redmine Items which are referenced inside [properties](#propertyDefinitions) or [fields](#fieldDeclarations) are automatically being removed when they are deleted.

The behaviour is type specific:
* When the type is an `array` the deleted item will just be removed from the array.
* When the type is no `array` but can be `undefined` it will be set to `undefined`.
* In all other cases an access is forbidden.

## <a name="stringInterpolations"></a> String Interpolations

RBO supports basic string interpolation in Single-Line and Multi-Line Strings.
As default each string literal is an interpolated string that may contain interpolation expressions. When an interpolated string is resolved to a result string, elements containing interpolation expressions are replaced by the string representations of the expression results.
A String Interpolation is defined as follows:
```
"Date: ${GetCurrentDateTime()}"
```

In the example the query invocation result of `GetCurrentDateTime()` is resolved to a result string which is replacing the interpolation expression.

To *escape* the `$` sign you can prefix it with the `` ` ``.

## <a name="arrayConcatanations"></a> Array Concatanations

RBO supports basic Array concatanations with the `+` sign.

The additive expression is defined as follows:
```
let array1: [int32] = [1, 2] + [3, 4]
let array2: [int32] = [1, 2] + 3
```

In the example the field `array1` is initialized with two arrays (`[1, 2]`, `[3, 4]`). Therefore `array1` contains in the end the values `[1, 2, 3, 4]`.
The second field `array2` is however assigned with one array `[1, 2]` and a single value `3`. Therefore the field `array2` contains in the end the values `[1, 2, 3]`.

## <a name="types"></a> Types

### <a name="array"></a> Array

An array is a list of elements of the type `T`. An array looks like this: `[T]`.

`T` can be any [Type](#types).

### <a name="enum"></a> Enum

An enumeration is a reusable type that has a name and contains a set of uniquely named constants.

The user can not declare own enums.

> Internally, enumerations are treated like Primitive Types. They represent the smallest possible type able to represent all defined Literal constants.

### <a name="primitiveTypes"></a> Primitive Types

RBO supports basic data types. The supported primitive types are:

|Type|Range|
|:-|:-|
|<a name="bool"></a>`bool`|false / true|
|<a name="date"></a>`date`|00:00:00.0000000 UTC, 1. Januar 0001 .. 23:59:59,9999999 UTC, 31. Dezember 9999|
|<a name="float32"></a>`float32`|-3.40282347E+38 .. 3.40282347E+38|
|<a name="int32"></a>`int32`|-2147483648 .. 2147483647|

### <a name="item"></a> Item

Items are the core element of **redmineBOOST**.

Not all Items are instantiable. The reason is that some can not be created through the provided REST API of Redmine or they are currently not supported.

Some Items can contain Sub-Items and therefore some can only be defined inside of specific Items.

It is forbidden to access a deleted Item. If a deleted Item was in an array, it is removed automatically from the array on property access. Nonetheless, a property which can be set to `undefined` will be `undefined` if the referenced item was deleted.

Example:
```
User {
    login: "mmustermann"
    firstname: "Max"
    lastname: "Mustermann"
    mail: "max.mustermann@example.com"
    status: UserStatus.Locked

    Authentication {
        password: "a1b2c3d4"
    }
}
```

### <a name="genericItem"></a> Generic Item

**redmineBOOST** supports generic items.
A generic item can use its type parameter `T` as the type of its return value or as the type of one of its properties.

Example:
```
Choice<string> {
    description: "Matrix"
    options: ["Blue Pill", "Red Pill"]
}
```

In the example the generic parameter was explicitely set to `string`. This sets the readonly property `value` and the element type of `options` to `string`. The property `options` is now of the type `[string]`.

### <a name="union"></a> Union

A union type describes a value that can be one of several types. 
We use the vertical bar (`|`) to separate each type, so `string | undefined` is the type of a value that can be a `string` or `undefined`.

### <a name="string"></a>String

The String type represents text as a sequence of UTF-16 code units.

A `string` is a sequential collection of characters that's used to represent text.

The `string` type can contain Multi-Line aswell as Single-Line text.

Because of [string interpolations](#stringInterpolations) the `$` sign has to be escaped by prefixing it with `` ` ``.

### <a name="restricted"></a> Restricted

The **redmineBOOST** Language has two special types, `restricted` and `undefined`, that have the values `restricted` and `undefined` respectively.
The Restricted type can only be the value `restricted` and occures if the user of the API key does not have the permission to access some properties.

### <a name="undefined"></a> Undefined

The Undefined type can only be the value `undefined` and occures if the property is of type `Union<undefined|...>` and does not exist. The result is an `undefined` value.

## <a name="literals"></a> Literals

RBO supports the following literal notations by example for each Primitive Type:

### <a name="arrayLiteral"></a>Array Literal

An array is a list of elements of the type `T`.

`T` can be an [Item Type](#item) or a [Primitive Type](#primitiveTypes).

```
[T]
```

### <a name="boolLiteral"></a>Boolean Literal

The Boolean Literal can only have the values `true` or `false`.

```
false
true
```

### <a name="dateLiteral"></a>Date Literal

The Date literal is always as follows: `(d|D)<Four-digit-year>-<two-digit-month>-<two-digit-day>`.

```
d2022-12-31
D2022-12-31
```

### <a name="float32Literal"></a>Float32 Literal
```
4.2
-2.1
+1.05
```

### <a name="int32Literal"></a>Int32 Literal
```
4
-2
+5
```

### <a name="restrictedLiteral"></a>Restricted Literal

Item Properties can have the value `restricted` if the user of the API key does not have the permission to access them.

```
restricted
```

### <a name="stringLiteral"></a>String Literal

There are two ways in declaring a string, Single-Line and Multi-Line. A Single-Line String always starts and ends with `"` and has to be declared in one line. A Multi-Line String however can be declared in multiple lines and always starts with `|"`. Furthermore, Multi-Line Strings will always append a linebreak.

Both string declarations allow [String Interpolations](#stringInterpolations).

Because of [string interpolations](#stringInterpolations) the `$` sign has to be escaped by prefixing it with `` ` ``.

```
// Single-Line String
"Hello, RBO!"

// Multi-Line String
|"Hello,
|"RBO!
```

### <a name="undefinedLiteral"></a>Undefined Literal

[Union types](#union) which can contain the [undefined type](#undefined) can be set to the `undefined` value.

```
undefined
```

## <a name="comments"></a> Comments

RBO supports Multi-line and Single-line comments. The Comments are ignored when executing the process description.

Comments can be used to explain specific design decisions.

A Multi-line comment is defined as follows:
```
/*
This is a
multi-line comment.
*/
```
A Single-line comment is defined as follows:
```
// This is a single-line comment.
```
