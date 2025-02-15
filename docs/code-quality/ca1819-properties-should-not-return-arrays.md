---
title: "CA1819: Properties should not return arrays"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "PropertiesShouldNotReturnArrays"
  - "CA1819"
helpviewer_keywords:
  - "PropertiesShouldNotReturnArrays"
  - "CA1819"
ms.assetid: 85fcf312-57f8-438a-8b10-34441fe0bdeb
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1819: Properties should not return arrays

|||
|-|-|
|TypeName|PropertiesShouldNotReturnArrays|
|CheckId|CA1819|
|Category|Microsoft.Performance|
|Breaking change|Breaking|

## Cause

A property returns an array.

By default, this rule only looks at externally visible properties and types, but this is [configurable](#configurability).

## Rule description

Arrays returned by properties are not write-protected, even if the property is read-only. To keep the array tamper-proof, the property must return a copy of the array. Typically, users won't understand the adverse performance implications of calling such a property. Specifically, they might use the property as an indexed property.

## How to fix violations

To fix a violation of this rule, either make the property a method or change the property to return a collection.

## When to suppress warnings

You can suppress a warning that's raised for a property of an attribute that's derived from the <xref:System.Attribute> class. Attributes can contain properties that return arrays, but can't contain properties that return collections.

You can suppress the warning if the property is part of a [Data Transfer Object (DTO)](/previous-versions/msp-n-p/ff649585(v=pandp.10)) class.

Otherwise, do not suppress a warning from this rule.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1819.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Performance). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Example violation

The following example shows a property that violates this rule:

[!code-csharp[FxCop.Performance.PropertyArrayViolation#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_1.cs)]
[!code-vb[FxCop.Performance.PropertyArrayViolation#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_1.vb)]

To fix a violation of this rule, either make the property a method or change the property to return a collection instead of an array.

### Change the property to a method

The following example fixes the violation by changing the property to a method:

[!code-vb[FxCop.Performance.PropertyArrayFixedMethod#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_2.vb)]
[!code-csharp[FxCop.Performance.PropertyArrayFixedMethod#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_2.cs)]

### Change the property to return a collection

The following example fixes the violation by changing the property to return a <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>:

[!code-csharp[FxCop.Performance.PropertyArrayFixedCollection#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_3.cs)]
[!code-vb[FxCop.Performance.PropertyArrayFixedCollection#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_3.vb)]

## Allow users to modify a property

You might want to allow the consumer of the class to modify a property. The following example shows a read/write property that violates this rule:

[!code-csharp[FxCop.Performance.PropertyModifyViolation#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_4.cs)]
[!code-vb[FxCop.Performance.PropertyModifyViolation#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_4.vb)]

The following example fixes the violation by changing the property to return a <xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName>:

[!code-vb[FxCop.Performance.PropertyModifyFixed#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_5.vb)]
[!code-csharp[FxCop.Performance.PropertyModifyFixed#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_5.cs)]

## Related rules

- [CA1024: Use properties where appropriate](../code-quality/ca1024-use-properties-where-appropriate.md)