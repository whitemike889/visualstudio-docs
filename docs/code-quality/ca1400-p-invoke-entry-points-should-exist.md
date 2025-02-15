---
title: "CA1400: P-Invoke entry points should exist"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA1400"
  - "PInvokeEntryPointsShouldExist"
helpviewer_keywords:
  - "PInvokeEntryPointsShouldExist"
  - "CA1400"
ms.assetid: 1d64e470-7b2f-4cca-8fb0-ac92829e6332
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1400: P/Invoke entry points should exist

|||
|-|-|
|TypeName|PInvokeEntryPointsShouldExist|
|CheckId|CA1400|
|Category|Microsoft.Interoperability|
|Breaking change|Non-breaking|

## Cause
A public or protected method is marked with the <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>. Either the unmanaged library could not be located or the method could not be matched to a function in the library. If the rule cannot find the method name exactly as it is specified, it looks for ANSI or wide-character versions of the method by suffixing the method name with 'A' or 'W'. If no match is found, the rule attempts to locate a function by using the __stdcall name format (_MyMethod@12, where 12 represents the length of the arguments). If no match is found, and the method name starts with '#', the rule searches for the function as an ordinal reference instead of a name reference.

## Rule description
No compile-time check is available to make sure that methods that are marked with <xref:System.Runtime.InteropServices.DllImportAttribute> are located in the referenced unmanaged DLL. If no function that has the specified name is  in the library, or the arguments to the method do not match the function arguments, the common language runtime throws an exception.

## How to fix violations
To fix a violation of this rule, correct the method that has the <xref:System.Runtime.InteropServices.DllImportAttribute> attribute. Make sure that the unmanaged library exists and is in the same directory as the assembly that contains the method. If the library is present and correctly referenced, verify that the method name, return type, and argument signature match the library function.

## When to suppress warnings
Do not suppress a warning from this rule when the unmanaged library is in the same directory as the managed assembly that references it. It might be safe to suppress a warning from this rule in the case where the unmanaged library could not be located.

## Example
The following example shows a type that violates the rule. No function that is named `DoSomethingUnmanaged` occurs in kernel32.dll.

[!code-csharp[FxCop.Interoperability.DLLExists#1](../code-quality/codesnippet/CSharp/ca1400-p-invoke-entry-points-should-exist_1.cs)]

## See also
 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>