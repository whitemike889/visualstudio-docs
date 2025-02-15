---
title: "CA1019: Define accessors for attribute arguments"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA1019"
  - "DefineAccessorsForAttributeArguments"
helpviewer_keywords:
  - "CA1019"
  - "DefineAccessorsForAttributeArguments"
ms.assetid: 197f2378-3c43-427e-80de-9ec25006c05c
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1019: Define accessors for attribute arguments

|||
|-|-|
|TypeName|DefineAccessorsForAttributeArguments|
|CheckId|CA1019|
|Category|Microsoft.Design|
|Breaking change|Non-breaking|

## Cause
In its constructor, an attribute defines arguments that do not have corresponding properties.

## Rule description
Attributes can define mandatory arguments that must be specified when you apply the attribute to a target. These are also known as positional arguments because they are supplied to attribute constructors as positional parameters. For every mandatory argument, the attribute should also provide a corresponding read-only property so that the value of the argument can be retrieved at execution time. This rule checks that for each constructor parameter, you have defined the corresponding property.

Attributes can also define optional arguments, which are also known as named arguments. These arguments are supplied to attribute constructors by name and should have a corresponding read/write property.

For mandatory and optional arguments, the corresponding properties and constructor parameters should use the same name but different casing. Properties use Pascal casing, and parameters use camel casing.

## How to fix violations
To fix a violation of this rule, add a read-only property for each constructor parameter that does not have one.

## When to suppress warnings
Suppress a warning from this rule if you do not want the value of the mandatory argument to be retrievable.

## Custom Attributes Example

The following example shows two attributes that define a mandatory (positional) parameter. The first implementation of the attribute is incorrectly defined. The second implementation is correct.

[!code-csharp[FxCop.Design.AttributeAccessors#1](../code-quality/codesnippet/CSharp/ca1019-define-accessors-for-attribute-arguments_1.cs)]
[!code-vb[FxCop.Design.AttributeAccessors#1](../code-quality/codesnippet/VisualBasic/ca1019-define-accessors-for-attribute-arguments_1.vb)]

## Positional and Named Arguments

Positional and named arguments make it clear to consumers of your library which arguments are mandatory for the attribute and which arguments are optional.

The following example shows an implementation of an attribute that has both positional and named arguments:

[!code-csharp[FxCop.Design.AttributeAccessorsNamed#1](../code-quality/codesnippet/CSharp/ca1019-define-accessors-for-attribute-arguments_2.cs)]

The following example shows how to apply the custom attribute to two properties:

[!code-csharp[FxCop.Design.AttributeAccessorsNamedApplied#1](../code-quality/codesnippet/CSharp/ca1019-define-accessors-for-attribute-arguments_3.cs)]

## Related rules
[CA1813: Avoid unsealed attributes](../code-quality/ca1813-avoid-unsealed-attributes.md)

## See also
[Attributes](/dotnet/standard/design-guidelines/attributes)