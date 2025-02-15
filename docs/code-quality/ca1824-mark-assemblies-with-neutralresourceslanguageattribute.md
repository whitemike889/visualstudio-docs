---
title: "CA1824: Mark assemblies with NeutralResourcesLanguageAttribute"
ms.date: 03/29/2018
ms.topic: reference
f1_keywords:
  - "CA1824"
  - "MarkAssembliesWithNeutralResourcesLanguage"
helpviewer_keywords:
  - "MarkAssembliesWithNeutralResourcesLanguage"
  - "CA1824"
ms.assetid: 10e97f8a-aa6e-47aa-b253-1e5d3a295d82
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1824: Mark assemblies with NeutralResourcesLanguageAttribute

|||
|-|-|
|TypeName|MarkAssembliesWithNeutralResourcesLanguage|
|CheckId|CA1824|
|Category|Microsoft.Performance|
|Breaking change|Non-breaking|

## Cause

An assembly contains a **ResX**-based resource but does not have the <xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=fullName> applied to it.

## Rule description

The <xref:System.Resources.NeutralResourcesLanguageAttribute> attribute informs the resource manager of an app's default culture. If the default culture's resources are embedded in the app's main assembly, and <xref:System.Resources.ResourceManager> has to retrieve resources that belong to the same culture as the default culture, the <xref:System.Resources.ResourceManager> automatically uses the resources located in the main assembly instead of searching for a satellite assembly. This bypasses the usual assembly probe, improves lookup performance for the first resource you load, and can reduce your working set.

> [!TIP]
> See [Packaging and deploying resources](/dotnet/framework/resources/packaging-and-deploying-resources-in-desktop-apps) for the process that <xref:System.Resources.ResourceManager> uses to probe for resource files.

## Fix violations

To fix a violation of this rule, add the attribute to the assembly, and specify the language of the resources of the neutral culture.

### To specify the neutral language for resources

1. In **Solution Explorer**, right-click your project, and then select **Properties**.

2. Select the **Application** tab, and then select **Assembly Information**.

   > [!NOTE]
   > If your project is a .NET Standard or .NET Core project, select the **Package** tab.

3. Select the language from the **Neutral language** or **Assembly neutral language** drop-down list.

4. Select **OK**.

## When to suppress warnings

It is permissible to suppress a warning from this rule. However, startup performance might degrade.

## See also

- <xref:System.Resources.NeutralResourcesLanguageAttribute>
- [Resources in desktop apps (.NET)](/dotnet/framework/resources/)
- [CA1703 - Resource strings should be spelled correctly](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)
- [CA1701 - Resource string compound words should be cased correctly](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)