---
title: "CA1024: Use properties where appropriate"
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
  - "UsePropertiesWhereAppropriate"
  - "CA1024"
helpviewer_keywords:
  - "CA1024"
  - "UsePropertiesWhereAppropriate"
ms.assetid: 3a04f765-af7c-4872-87ad-9cc29e8e657f
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1024: Use properties where appropriate

|||
|-|-|
|TypeName|UsePropertiesWhereAppropriate|
|CheckId|CA1024|
|Category|Microsoft.Design|
|Breaking change|Breaking|

## Cause

A method has a name that starts with `Get`, takes no parameters, and returns a value that is not an array.

By default, this rule only looks at public and protected methods, but this is [configurable](#configurability).

## Rule description

In most cases, properties represent data and methods perform actions. Properties are accessed like fields, which makes them easier to use. A method is a good candidate to become a property if one of these conditions is present:

- Takes no arguments and returns the state information of an object.

- Accepts a single argument to set some part of the state of an object.

Properties should behave as if they are fields; if the method cannot, it should not be changed to a property. Methods are better than properties in the following situations:

- The method performs a time-consuming operation. The method is perceivably slower than the time that is required to set or get the value of a field.

- The method performs a conversion. Accessing a field does not return a converted version of the data that it stores.

- The Get method has an observable side effect. Retrieving the value of a field does not produce any side effects.

- The order of execution is important. Setting the value of a field does not rely on the occurrence of other operations.

- Calling the method two times in succession creates different results.

- The method is static but returns an object that can be changed by the caller. Retrieving the value of a field does not allow the caller to change the data that is stored by the field.

- The method returns an array.

## How to fix violations

To fix a violation of this rule, change the method to a property.

## When to suppress warnings

Suppress a warning from this rule if the method meets at least one of the previously listed criteria.

## Configurability

If you're running this rule from [FxCop analyzers](install-fxcop-analyzers.md) (and not with legacy analysis), you can configure which parts of your codebase to run this rule on, based on their accessibility. For example, to specify that the rule should run only against the non-public API surface, add the following key-value pair to an .editorconfig file in your project:

```ini
dotnet_code_quality.ca1024.api_surface = private, internal
```

You can configure this option for just this rule, for all rules, or for all rules in this category (Design). For more information, see [Configure FxCop analyzers](configure-fxcop-analyzers.md).

## Control property expansion in the debugger

One reason programmers avoid using a property is because they do not want the debugger to autoexpand it. For example, the property might involve allocating a large object or calling a P/Invoke, but it might not actually have any observable side effects.

You can prevent the debugger from autoexpanding properties by applying <xref:System.Diagnostics.DebuggerBrowsableAttribute?displayProperty=fullName>. The following example shows this attribute being applied to an instance property.

```vb
Imports System
Imports System.Diagnostics

Namespace Microsoft.Samples

    Public Class TestClass

        ' [...]

        <DebuggerBrowsable(DebuggerBrowsableState.Never)> _
        Public ReadOnly Property LargeObject() As LargeObject
            Get
                ' Allocate large object
                ' [...]
            End Get
        End Property

    End Class

End Namespace
```

```csharp
using System;
using System.Diagnostics;

namespace Microsoft.Samples
{
    publicclass TestClass
    {
        // [...]

        [DebuggerBrowsable(DebuggerBrowsableState.Never)]
        public LargeObject LargeObject
        {
            get
            {
                // Allocate large object
                // [...]
            }
        }
    }
}
```

## Example

The following example contains several methods that should be converted to properties and several that should not because they don't behave like fields.

[!code-csharp[FxCop.Design.MethodsProperties#1](../code-quality/codesnippet/CSharp/ca1024-use-properties-where-appropriate_1.cs)]