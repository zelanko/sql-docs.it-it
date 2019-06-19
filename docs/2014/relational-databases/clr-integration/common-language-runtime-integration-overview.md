---
title: Panoramica di Common Language Runtime (CLR) Integration | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- managed code [SQL Server]
- common language runtime [SQL Server], about CLR integration
- cross-language integration
- integrating CLR [SQL Server]
- .NET Framework [SQL Server], common language runtime
- code access security [CLR integration]
- managed code [SQL Server], CLR integration
ms.assetid: 7be9e644-36a2-48fc-9206-faf59fdff4d7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a7764c6e8e45b56e43e592e70b1c85b8d4744b69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919311"
---
# <a name="common-language-runtime-clr-integration-overview"></a>Panoramica dell'integrazione con CLR (Common Language Runtime)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] include ora l'integrazione del componente CRL (Common Language Runtime) di .NET Framework per [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. CLR fornisce codice gestito con servizi quali l'integrazione tra linguaggi diversi, la sicurezza da accesso di codice, la gestione della durata degli oggetti e il supporto per il debug e il profiling. Grazie all'integrazione con Common Language Runtime, gli sviluppatori di applicazioni e gli utenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hanno ora la possibilità di scrivere stored procedure, trigger, tipi definiti dall'utente, funzioni definite dall'utente (scalari e con valori di tabella) e funzioni di aggregazione definite dall'utente utilizzando qualsiasi linguaggio di .NET Framework, inclusi [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] include la versione preinstallata di 4 di .NET Framework.  
  
 I vantaggi principali di questa integrazione sono i seguenti:  
  
-   **Un modello di programmazione migliore.** I linguaggi .NET Framework sono sotto molti aspetti più completi di Transact-SQL, in quanto offrono costrutti e funzionalità precedentemente non disponibili per gli sviluppatori di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. È possibile inoltre sfruttare la potenza della libreria .NET Framework che fornisce una vasta gamma di classi, utilizzabili in modo rapido ed efficiente per risolvere i problemi di programmazione.  
  
-   **Miglioramento della sicurezza e protezione.** Il codice gestito è in esecuzione in un ambiente CLR, ospitato dal motore di database. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] lo utilizza per fornire un'alternativa più sicura alle stored procedure estese disponibili in versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   **Possibilità di definire i tipi di dati e funzioni di aggregazione.** I tipi definiti dall'utente e le funzioni di aggregazione definite dall'utente sono due nuovi oggetti di database gestiti che espandono le capacità di archiviazione ed esecuzione di query di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   **Sviluppo semplificato attraverso un ambiente standardizzato.** Lo sviluppo di database è integrato nelle versioni future dell'ambiente di sviluppo di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio .NET. Gli sviluppatori utilizzano per lo sviluppo e il debug degli script e degli oggetti di database gli stessi strumenti impiegati per scrivere componenti e servizi .NET Framework di livello intermedio o di livello client.  
  
-   **Possibilità di migliorare le prestazioni e scalabilità.** In molte situazioni, i modelli di compilazione ed esecuzione del linguaggio .NET Framework consentono di ottenere prestazioni migliori rispetto a Transact-SQL.  
  
 Nella tabella seguente sono elencati gli argomenti inclusi in questa sezione.  
  
 [Panoramica dell'integrazione con CLR](clr-integration-overview.md)  
 Vengono descritti i tipi di oggetti che è possibile compilare utilizzando l'integrazione con CLR e vengono esaminati i requisiti per la compilazione di oggetti di database tramite questa integrazione.  
  
 [Novità dell'integrazione con CLR](clr-integration-what-s-new.md)  
 Vengono descritte le nuove caratteristiche di questa versione.  
  
 [Architettura dell'integrazione con CLR](../../database-engine/dev-guide/architecture-of-clr-integration.md)  
 Vengono illustrati gli obiettivi di progettazione dell'integrazione con CLR.  
  
 [Abilitazione dell'integrazione con CLR](clr-integration-enabling.md)  
 Viene illustrato come abilitare l'integrazione con CLR.  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione di .NET Framework](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [Prestazioni dell'integrazione con CLR](clr-integration-architecture-performance.md)  
  
  
