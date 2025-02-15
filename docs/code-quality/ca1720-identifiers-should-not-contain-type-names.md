---
title: "CA1720: Identifiers should not contain type names"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "CA1720"
  - "IdentifiersShouldNotContainTypeNames"
helpviewer_keywords:
  - "IdentifiersShouldNotContainTypeNames"
  - "CA1720"
ms.assetid: c95ee48f-f23a-45f0-ac9e-a3c1ecfabdea
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1720: Identifiers should not contain type names

|||
|-|-|
|TypeName|IdentifiersShouldNotContainTypeNames|
|CheckId|CA1720|
|Category|Microsoft.Naming|
|Breaking change|Breaking|

## Cause

The name of a parameter in a member contains a data type name.

-or-

The name of a member contains a language-specific data type name.

By default, this rule only looks at externally visible members, but this is [configurable](#configurability).

## Rule description

Names of parameters and members are better used to communicate their meaning than to describe their type, which is expected to be provided by development tools. For names of members, if a data type name must be used, use a language-independent name instead of a language-specific one. For example, instead of the C# type name `int`, use the language-independent data type name, `Int32`.

Each discrete token in the name of the parameter or member is checked against the following language-specific data type names in a case-insensitive manner:

- Bool
- WChar
- Int8
- UInt8
- Short
- UShort
- Int
- UInt
- Integer
- UInteger
- Long
- ULong
- Unsigned
- Signed
- Float
- Float32
- Float64

In addition, the names of a parameter are also checked against the following language-independent data type names in a case-insensitive manner:

- Object
- Obj
- Boolean
- Char
- String
- SByte
- Byte
- UByte
- Int16
- UInt16
- Int32
- UInt32
- Int64
- UInt64
- IntPtr
- Ptr
- Pointer
- UInptr
- UPtr
- UPointer
- Single
- Double
- Decimal
- Guid

## How to fix violations

**If fired against a parameter:**

Replace the data type identifier in the name of the parameter with either a term that better describes its meaning or a more generic term, such as 'value'.

**If fired against a member:**

Replace the language-specific data type identifier in the name of the member with a term that better describes its meaning, a language-independent equivalent, or a more generic term, such as 'value'.

## When to suppress warnings

Occasional use of type-based parameter and member names might be appropriate. However, for new development, no known scenarios occur where you should suppress a warning from this rule. For libraries that have previously shipped, you might have to suppress a warning from this rule.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1720.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Naming). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Related rules

- [CA1709: Identifiers should be cased correctly](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
- [CA1708: Identifiers should differ by more than case](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)
- [CA1707: Identifiers should not contain underscores](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)
- [CA1719: Parameter names should not match member names](../code-quality/ca1719-parameter-names-should-not-match-member-names.md)