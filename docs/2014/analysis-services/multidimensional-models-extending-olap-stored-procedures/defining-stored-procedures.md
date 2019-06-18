---
title: Definizione delle Stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services]
- OLAP [Analysis Services], stored procedures
- external routines [Analysis Services]
- stored procedures [Analysis Services], about stored procedures
ms.assetid: f9c57d91-f60f-4f0e-8f7f-d87f4ba97b7c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 69daca3a13cf5318e102002f0edfcb98b80ff9d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702764"
---
# <a name="defining-stored-procedures"></a>Definizione delle stored procedure
  È possibile usare le stored procedure da chiamare routine esterne da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. È possibile scrivere una routine esterna chiamata da una stored procedure in ogni linguaggio di Common Runtime Language (CLR), ad esempio C, C++, C#, Visual Basic o Visual Basic .NET. Una stored procedure può essere creata una volta e chiamata da vari contesti, ad esempio da altre stored procedure, da misure calcolate o da applicazioni client. Consentendo di sviluppare il codice comune una sola volta e di archiviarlo in una singola posizione, le stored procedure semplificano le operazioni di sviluppo e di implementazione del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Possono essere utilizzate per aggiungere alle applicazioni funzionalità business non presenti in quelle native di MDX.  
  
 In questa sezione vengono fornite le informazioni necessarie per comprendere, progettare e implementare stored procedure.  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Progettazione di stored procedure](../multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|Descrive la procedura per progettare assembly da utilizzare con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Creazione di stored procedure](creating-stored-procedures.md)|Descrive la procedura per creare assembly per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Esecuzione di chiamate a stored procedure](calling-stored-procedures.md)|Offre informazioni sull'utilizzo degli assembly in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Accesso al contesto di query nelle stored procedure](accessing-query-context-in-stored-procedures.md)|Descrive la procedura per accedere alle informazioni sul contesto e l'ambito con gli assembly.|  
|[Impostazione della sicurezza per stored procedure](setting-security-for-stored-procedures.md)|Descrive la procedura per configurare la sicurezza degli assembly in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Debug di stored procedure](debugging-stored-procedures.md)|Descrive la procedura per eseguire il debug degli assembly in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di assembly di modelli multidimensionali](../multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
