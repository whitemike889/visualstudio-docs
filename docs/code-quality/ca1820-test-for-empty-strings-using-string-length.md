---
title: "CA1820: Test for empty strings using string length"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "TestForEmptyStringsUsingStringLength"
  - "CA1820"
helpviewer_keywords:
  - "TestForEmptyStringsUsingStringLength"
  - "CA1820"
ms.assetid: da1e70c8-b1dc-46b9-8b8f-4e6e48339681
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1820: Test for empty strings using string length

|||
|-|-|
|TypeName|TestForEmptyStringsUsingStringLength|
|CheckId|CA1820|
|Category|Microsoft.Performance|
|Breaking change|Non-breaking|

## Cause

A string is compared to the empty string by using <xref:System.Object.Equals%2A?displayProperty=nameWithType>.

## Rule description

Comparing strings using the <xref:System.String.Length%2A?displayProperty=nameWithType> property or the <xref:System.String.IsNullOrEmpty%2A?displayProperty=nameWithType> method is faster than using <xref:System.Object.Equals%2A>. This is because <xref:System.Object.Equals%2A> executes significantly more MSIL instructions than either <xref:System.String.IsNullOrEmpty%2A> or the number of instructions executed to retrieve the <xref:System.String.Length%2A> property value and compare it to zero.

For null strings, <xref:System.Object.Equals%2A> and `<string>.Length == 0` behave differently. If you try to get the value of the <xref:System.String.Length%2A> property on a null string, the common language runtime throws a <xref:System.NullReferenceException?displayProperty=fullName>. If you perform a comparison between a null string and the empty string, the common language runtime does not throw an exception and returns `false`. Testing for null does not significantly affect the relative performance of these two approaches. When targeting .NET Framework 2.0 or later, use the <xref:System.String.IsNullOrEmpty%2A> method. Otherwise, use the <xref:System.String.Length%2A> == 0 comparison whenever possible.

## How to fix violations

To fix a violation of this rule, change the comparison to use the <xref:System.String.IsNullOrEmpty%2A> method.

## When to suppress warnings

It's safe to suppress a warning from this rule if performance is not an issue.

## Example

The following example illustrates the different techniques that are used to look for an empty string.

[!code-csharp[FxCop.Performance.StringTest#1](../code-quality/codesnippet/CSharp/ca1820-test-for-empty-strings-using-string-length_1.cs)]