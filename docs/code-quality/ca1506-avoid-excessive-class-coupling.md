---
title: "CA1506: Avoid excessive class coupling"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "AvoidExcessiveClassCoupling"
  - "CA1506"
helpviewer_keywords:
  - "AvoidExcessiveClassCoupling"
  - "CA1506"
ms.assetid: 9f0943c0-e802-4e3f-8798-2ab8653ddc80
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1506: Avoid excessive class coupling

|||
|-|-|
|TypeName|AvoidExcessiveClassCoupling|
|CheckId|CA1506|
|Category|Microsoft.Maintainability|
|Breaking change|Breaking|

## Cause

A type or method is coupled with many other types.

## Rule description

This rule measures class coupling by counting the number of unique type references that a type or method contains.

Types and methods that have a high degree of class coupling can be difficult to maintain. It's a good practice to have types and methods that exhibit low coupling and high cohesion.

## How to fix violations

To fix this violation, try to redesign the type or method to reduce the number of types to which it's coupled.

## When to suppress warnings

Exclude this warning when the type or method is considered maintainable despite its large number of dependencies on other types.

## See also

- [Maintainability Warnings](../code-quality/maintainability-warnings.md)
- [Measuring Complexity and Maintainability of Managed Code](../code-quality/code-metrics-values.md)