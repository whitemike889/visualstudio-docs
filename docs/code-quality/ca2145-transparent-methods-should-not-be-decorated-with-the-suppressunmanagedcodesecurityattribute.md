---
title: "CA2145: Transparent methods should not be decorated with the SuppressUnmanagedCodeSecurityAttribute"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA2145"
ms.assetid: 81970700-b438-4b3b-9239-16887e16f7b7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA2145: Transparent methods should not be decorated with the SuppressUnmanagedCodeSecurityAttribute

|||
|-|-|
|TypeName|TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity|
|CheckId|CA2145|
|Category|Microsoft.Security|
|Breaking change|Breaking|

## Cause

A transparent method, a method that is marked with the <xref:System.Security.SecuritySafeCriticalAttribute> method, or a type that contains a method is marked with the <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> attribute.

## Rule description

Methods decorated with the <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> attribute have an implicit LinkDemand placed upon any method that calls it. This LinkDemand requires that the calling code be security critical. Marking the method that uses SuppressUnmanagedCodeSecurity with the <xref:System.Security.SecurityCriticalAttribute> attribute makes this requirement more obvious for callers of the method.

## How to fix violations

To fix a violation of this rule, mark the method or type with the <xref:System.Security.SecurityCriticalAttribute> attribute.

## When to suppress warnings

Do not suppress a warning from this rule.

### Code

[!code-csharp[FxCop.Security.CA2145.TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity#1](../code-quality/codesnippet/CSharp/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute_1.cs)]