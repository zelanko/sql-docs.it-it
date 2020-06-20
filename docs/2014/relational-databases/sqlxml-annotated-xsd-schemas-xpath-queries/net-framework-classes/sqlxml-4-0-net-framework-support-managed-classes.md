---
title: Classi gestite SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- .NET Framework [SQLXML], Managed Classes
- SQL Server .NET Data Provider
- Managed Classes [SQLXML], about managed classes
- providers [SQLXML], SQL Server .NET Data Provider
- data providers [SQLXML], SQL Server .NET Data Provider
- Managed Classes [SQLXML]
- XML [SQLXML]
- SQLXML Managed Classes
- providers [SQLXML], SQLXML Managed Classes
- data providers [SQLXML], SQLXML Managed Classes
- SQLXML, Managed Classes
ms.assetid: 73a5faeb-dabf-4895-acb5-a9651b646065
author: rothja
ms.author: jroth
ms.openlocfilehash: bb8d2d4f2d2fc512901e4ad37f0e46cf696b9475
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85015276"
---
# <a name="sqlxml-managed-classes"></a>classi gestite SQLXML
  Le classi gestite [!INCLUDE[msCoName](../../../includes/msconame-md.md)] espongono la funzionalità di SQLXML 4.0 in [!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework. Le classi gestite SQLXML consentono di scrivere un'applicazione C# per accedere ai dati XML da un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], portare i dati nell'ambiente .NET Framework, elaborare i dati e inviare nuovamente gli aggiornamenti a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come DiffGram per applicarli. Quando si applicano aggiornamenti a un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando le classi gestite SQLXML, è necessario utilizzare uno schema di mapping. Per un esempio funzionante, vedere [accesso alla funzionalità SQLXML nell'ambiente .NET](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 Per utilizzare le classi gestite SQLXML con SQLXML 4.0, è necessario installare Microsoft Visual Studio.  
  
> [!NOTE]  
>  .NET Framework include il provider di dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .NET. Tale provider può essere utilizzato per accedere a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dall'ambiente .NET. È tuttavia in grado di gestire solo query SQL tradizionali (ovvero query del database relazionale ad eccezione delle query FOR XML). Non è possibile eseguire modelli XML o query XPath sul lato server in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Modello a oggetti di classi gestite SQLXML](../../../database-engine/dev-guide/sqlxml-managed-classes-object-model.md)  
 Vengono documentate le classi gestite SQLXML e le proprietà e i metodi rispettivi.  
  
 [Utilizzo di classi gestite SQLXML](sqlxml-4-0-net-framework-support-managed-classes.md)  
 Vengono forniti esempi di utilizzo delle classi gestite SQLXML.  
  
  
