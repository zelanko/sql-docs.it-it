---
title: Assembly (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration]
- assemblies [CLR integration], about assemblies
- managed code [SQL Server], assemblies
ms.assetid: 4b146437-3061-47f6-9e8c-26eeea10b54e
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ebd47e354b77a57768a396b2c5d5dd8e3c570d2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954245"
---
# <a name="assemblies-database-engine"></a>Assembly (Motore di database)
  Gli argomenti di questa sezione includono informazioni utili per comprendere, progettare e implementare assembly.  
  
 Gli assembly sono file DLL utilizzati in un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per distribuire funzioni, stored procedure, trigger, funzioni di aggregazione definite dall'utente e tipi definiti dall'utente scritti in uno dei linguaggi di codice gestito ospitati dal [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR), anziché in [!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
 Un assembly di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è un oggetto che fa riferimento a un modulo di applicazione gestito (file con estensione dll) creato nel linguaggio CLR di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Un assembly contiene i metadati della classe e codice gestito. Il caricamento di un assembly in un'istanza di SQL Server è il primo passaggio da eseguire per creare uno degli oggetti di database seguenti:  
  
-   Funzioni CLR. Per altre informazioni, vedere [create CLR Functions](../user-defined-functions/create-clr-functions.md).  
  
-   Stored procedure CLR. Per ulteriori informazioni, vedere [stored procedure CLR](../../database-engine/dev-guide/clr-stored-procedures.md).  
  
-   Trigger CLR. Per altre informazioni, vedere [create CLR Triggers](../triggers/create-clr-triggers.md).  
  
-   Funzioni di aggregazione definite dall'utente. Per altre informazioni, vedere [creare funzioni di aggregazione definite dall'utente](../user-defined-functions/create-user-defined-aggregates.md).  
  
-   Tipi definiti dall'utente. Per altre informazioni, vedere [Uso dei tipi definiti dall'utente](../native-client/features/using-user-defined-types.md).  
  
 Gli assembly svolgono le funzioni seguenti in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Includono il codice gestito che esegue le funzionalità di uno o più degli oggetti di database CLR elencati in precedenza.  
  
-   Contengono i metadati che includono il numero di versione e la lingua dell'assembly, una chiave pubblica facoltativa che identifica l'elenco delle classi dell'assembly, i metodi definiti nell'assembly e l'architettura del processore dell'assembly.  
  
-   Gestiscono il livello di accesso del codice gestito alle risorse esterne tramite l'impostazione delle autorizzazioni di accesso per il codice.  
  
-   Includono i metadati relativi alle dipendenze da altri assembly a cui viene fatto riferimento nell'assembly.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Description|  
|-----------|-----------------|  
|[Progettazione di assembly](assemblies-designing.md)|Descrive gli elementi da tenere in considerazione prima di creare un assembly, che includono l'assemblaggio degli assembly, le autorizzazioni di accesso per il codice e altre restrizioni.|  
|[Implementazione di assembly](assemblies-implementing.md)|Illustra come creare ed eliminare gli assembly, come e quando modificare gli assembly e come recuperare i metadati relativi agli assembly.|  
|[Recupero di informazioni sugli assembly](assemblies-getting-information.md)|Elenca le viste del catalogo e le funzioni sulle quali è possibile eseguire query relative agli assembly.|  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi alla programmazione dell'integrazione con CLR &#40;Common Language Runtime&#41;](common-language-runtime-clr-integration-programming-concepts.md)  
  
  
