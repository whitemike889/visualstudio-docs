---
title: "CA1016: Mark assemblies with AssemblyVersionAttribute"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "MarkAssembliesWithAssemblyVersion"
  - "CA1016"
helpviewer_keywords:
  - "CA1016"
  - "MarkAssembliesWithAssemblyVersion"
ms.assetid: 4340aed8-d92b-4cde-a398-cb6963c6da5a
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CPP
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1016: Mark assemblies with AssemblyVersionAttribute

|||
|-|-|
|TypeName|MarkAssembliesWithAssemblyVersion|
|CheckId|CA1016|
|Category|Microsoft.Design|
|Breaking change|Non-breaking|

## Cause

The assembly does not have a version number.

## Rule description

The identity of an assembly is composed of the following information:

- Assembly name

- Version number

- Culture

- Public key (for strongly named assemblies).

.NET uses the version number to uniquely identify an assembly and to bind to types in strongly named assemblies. The version number is used together with version and publisher policy. By default, applications run only with the assembly version with which they were built.

## How to fix violations

To fix a violation of this rule, add a version number to the assembly by using the <xref:System.Reflection.AssemblyVersionAttribute?displayProperty=fullName> attribute.

## When to suppress warnings

Do not suppress a warning from this rule for assemblies that are used by third parties or in a production environment.

## Example

The following example shows an assembly that has the <xref:System.Reflection.AssemblyVersionAttribute> attribute applied.

[!code-csharp[FxCop.Design.AssembliesVersion#1](../code-quality/codesnippet/CSharp/ca1016-mark-assemblies-with-assemblyversionattribute_1.cs)]
[!code-vb[FxCop.Design.AssembliesVersion#1](../code-quality/codesnippet/VisualBasic/ca1016-mark-assemblies-with-assemblyversionattribute_1.vb)]
[!code-cpp[FxCop.Design.AssembliesVersion#1](../code-quality/codesnippet/CPP/ca1016-mark-assemblies-with-assemblyversionattribute_1.cpp)]

## See also

- [Assembly versioning](/dotnet/framework/app-domains/assembly-versioning)
- [How to: Create a publisher policy](/dotnet/framework/configure-apps/how-to-create-a-publisher-policy)