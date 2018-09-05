---
title: "CA2139: Transparent methods may not use the HandleProcessCorruptingExceptions attribute | Microsoft Docs"
ms.custom: ""
ms.date: "2018-06-30"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "vs-devops-test"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords:
  - "CA2139"
ms.assetid: 45a0328a-add7-40f9-8934-dff59beb02b3
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: "wpickett"
---
# CA2139: Transparent methods may not use the HandleProcessCorruptingExceptions attribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

The latest version of this topic can be found at [CA2139: Transparent methods may not use the HandleProcessCorruptingExceptions attribute](https://docs.microsoft.com/visualstudio/code-quality/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute).

|||
|-|-|
|TypeName|TransparentMethodsMustNotHandleProcessCorruptingExceptions|
|CheckId|CA2139|
|Category|Microsoft.Security|
|Breaking Change|Breaking|

## Cause
 A transparent method is marked with the <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> attribute.

## Rule Description
 This rule fires any method which is transparent and attempts to handle a process corrupting exception by using the <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> attribute. A process corrupting exception is a CLR version 4.0 exception classification of exceptions such <xref:System.AccessViolationException>. The HandleProcessCorruptedStateExceptionsAttribute attribute may only be used by security critical methods, and will be ignored if it is applied to a transparent method. To handle process corrupting exceptions, this method must become security critical or security safe-critical.

## How to Fix Violations
 To fix a violation of this rule, remove the <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> attribute, or mark the method with the <xref:System.Security.SecurityCriticalAttribute> or the <xref:System.Security.SecuritySafeCriticalAttribute> attribute.

## When to Suppress Warnings
 Do not suppress a warning from this rule.

## Example
 In this example, a transparent method is marked with the <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> attribute and will fail the rule. The method should also be marked with the <xref:System.Security.SecurityCriticalAttribute> or the <xref:System.Security.SecuritySafeCriticalAttribute> attribute.

 [!code-csharp[FxCop.Security.CA2139.TransparentMethodsMustNotHandleProcessCorruptingExceptions#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2139.transparentmethodsmustnothandleprocesscorruptingexceptions/cs/ca2139 - transparentmethodsmustnothandleprocesscorruptingexceptions.cs#1)]


