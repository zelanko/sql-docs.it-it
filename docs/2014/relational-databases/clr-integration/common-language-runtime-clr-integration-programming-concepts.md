---
title: Concetti relativi alla programmazione dell'integrazione con CLR (Common Language Runtime) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- CLR [SQL Server] See common language runtime [SQL Server]
- Database Engine [SQL Server], .NET Framework
- .NET Framework [SQL Server], Database Engine programming
- common language runtime [SQL Server]
- .NET Framework [SQL Server]
ms.assetid: 951bf851-3e6e-4361-ae6a-2bcd5b837ebd
author: rothja
ms.author: jroth
ms.openlocfilehash: 6de928980da1310433832670abc8175205613cdc
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970729"
---
# <a name="common-language-runtime-clr-integration-programming-concepts"></a>Concetti relativi alla programmazione dell'integrazione con CLR (Common Language Runtime)
  A partire da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è inclusa l'integrazione del componente CRL (Common Language Runtime) di .NET Framework per [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. È pertanto possibile scrivere stored procedure, trigger, tipi definiti dall'utente, funzioni definite dall'utente, funzioni di aggregazione definite dall'utente e funzioni di flusso con valori di tabella usando qualsiasi linguaggio di .NET Framework, inclusi [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#.  
  
 Lo spazio dei nomi Microsoft.SqlServer.Server include la funzionalità principali per la programmazione CLR in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Lo spazio dei nomi Microsoft.SqlServer.Server, tuttavia, viene trattato nella documentazione di .NET Framework SDK. Questa documentazione non è inclusa nella documentazione online di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Per impostazione predefinita, durante l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene installato .NET Framework, ma non .NET Framework SDK. Se SDK non è installato nel computer né incluso nella raccolta della documentazione online, i collegamenti al contenuto SDK presenti in questa sezione non funzionano. Installare .NET Framework SDK, Al termine dell'installazione, aggiungere l'SDK alla raccolta della documentazione online e al sommario seguendo le istruzioni riportate in [installazione di .NET Framework SDK](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx).  
  
 Nella tabella seguente vengono elencati gli argomenti disponibili in questa sezione.  
  
 [Panoramica dell'integrazione di Common Language Runtime &#40;CLR&#41;](common-language-runtime-integration-overview.md)  
 Viene fornita una breve panoramica di CLR e vengono descritti i motivi e le modalità dell'utilizzo di questa tecnologia in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Vengono inoltre descritti i vantaggi dell'utilizzo di CLR per creare oggetti di database.  
  
 [Assembly &#40;Motore di database&#41;](assemblies-database-engine.md)  
 Viene descritto come usare gli assembly in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per distribuire funzioni, stored procedure, trigger, aggregazioni definite dall'utente e tipi definiti dall'utente scritti usando uno dei linguaggi di codice gestito di Common Language Runtime (CLR) di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework e non [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 [Compilazione di oggetti di database con Common Language Runtime &#40;integrazione&#41; CLR](database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)  
 Vengono descritti i tipi di oggetti che è possibile compilare usando CLR e vengono esaminati i requisiti per la compilazione di oggetti di database CLR.  
  
 [Accesso ai dati da oggetti di database CLR](data-access/data-access-from-clr-database-objects.md)  
 Viene descritto il modo in cui una routine CLR può accedere a dati archiviati in un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Sicurezza per l'integrazione con CLR](security/clr-integration-security.md)  
 Viene descritto il modello di sicurezza dell'integrazione CLR.  
  
 [Debug di oggetti di database CLR](debugging-clr-database-objects.md)  
 Vengono descritte le limitazioni e i requisiti per il debug di oggetti di database CLR.  
  
 [Distribuzione di oggetti di database CLR](deploying-clr-database-objects.md)  
 Viene descritta la distribuzione di assembly in server di produzione.  
  
 [Gestione degli assembly dell'integrazione con CLR](assemblies/managing-clr-integration-assemblies.md)  
 Viene descritto come creare ed eliminare assembly di integrazione CLR.  
  
 [Monitoraggio e risoluzione dei problemi relativi agli oggetti di database gestiti](monitoring-and-troubleshooting-managed-database-objects.md)  
 Vengono fornite informazioni sugli strumenti che è possibile usare per monitorare e risolvere i problemi relativi agli oggetti di database e agli assembly gestiti in esecuzione in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Scenari di utilizzo ed esempi per l'integrazione con CLR &#40;Common Language Runtime&#41;](../../database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
 Vengono descritti gli scenari di utilizzo e gli esempi di codice che usano oggetti CLR.  
  
## <a name="see-also"></a>Vedere anche  
 [Assembly &#40;motore di database&#41;](assemblies-database-engine.md)   
 [Installazione di .NET Framework SDK](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)  
  
  
