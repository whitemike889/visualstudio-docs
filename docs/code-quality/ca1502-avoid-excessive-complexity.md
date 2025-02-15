---
title: "CA1502: Avoid excessive complexity"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "AvoidExcessiveComplexity"
  - "CA1502"
helpviewer_keywords:
  - "CA1502"
  - "AvoidExcessiveComplexity"
ms.assetid: d735454b-2f8f-47ce-907d-f7a5a5391221
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
# CA1502: Avoid excessive complexity

|||
|-|-|
|TypeName|AvoidExcessiveComplexity|
|CheckId|CA1502|
|Category|Microsoft.Maintainability|
|Breaking change|Non-breaking|

## Cause

A method has an excessive cyclomatic complexity.

## Rule description

*Cyclomatic complexity* measures the number of linearly independent paths through the method, which is determined by the number and complexity of conditional branches. A low cyclomatic complexity generally indicates a method that is easy to understand, test, and maintain. The cyclomatic complexity is calculated from a control flow graph of the method and is given as follows:

cyclomatic complexity = the number of edges - the number of nodes + 1

A *node* represents a logic branch point and an *edge* represents a line between nodes.

The rule reports a violation when the cyclomatic complexity is more than 25.

You can learn more about code metrics at [Measure complexity of managed code](../code-quality/code-metrics-values.md).

## How to fix violations

To fix a violation of this rule, refactor the method to reduce its cyclomatic complexity.

## When to suppress warnings

It is safe to suppress a warning from this rule if the complexity cannot easily be reduced and the method is easy to understand, test, and maintain. In particular, a method that contains a large `switch` (`Select` in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) statement is a candidate for exclusion. The risk of destabilizing the code base late in the development cycle or introducing an unexpected change in run-time behavior in previously shipped code might outweigh the maintainability benefits of refactoring the code.

## How Cyclomatic complexity is calculated

The cyclomatic complexity is calculated by adding 1 to the following:

- Number of branches (such as `if`, `while`, and `do`)

- Number of `case` statements in a `switch`

## Example

The following examples show methods that have varying cyclomatic complexities.

**Cyclomatic complexity of 1**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_1.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_1.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_1.cs)]

## Example

**Cyclomatic complexity of 2**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_2.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_2.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_2.cs)]

## Example

**Cyclomatic complexity of 3**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_3.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_3.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_3.cs)]

## Example

**Cyclomatic complexity of 8**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_4.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_4.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_4.cs)]

## Related rules

[CA1501: Avoid excessive inheritance](../code-quality/ca1501-avoid-excessive-inheritance.md)

## See also

- [Measuring Complexity and Maintainability of Managed Code](../code-quality/code-metrics-values.md)