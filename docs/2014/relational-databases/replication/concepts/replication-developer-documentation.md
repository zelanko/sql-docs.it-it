---
title: Per gli sviluppatori&#39;Guida (replica) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- developer's guide [SQL Server replication]
- programming [SQL Server replication]
- replication [SQL Server], development
ms.assetid: 7ee134ae-1cab-4a35-8017-8ac6d8fc64b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 499edc588b4253b3ae37c2be0bcde1cbbd79dea6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777823"
---
# <a name="developer39s-guide-replication"></a>Per gli sviluppatori&#39;Guida (replica)
  La possibilità da configurare, gestire e monitorare a livello di codice una topologia di replica consente di semplificare le attività di replica ripetute e di migliorare l'esperienza utente per le applicazioni basate sulla replica. Mediante la programmazione della replica, è possibile offrire funzionalità di replica personalizzate agli utenti finali, senza che sia necessario conoscere le stored procedure di replica e i file eseguibili degli agenti di replica o utilizzare l'interfaccia di replica implementata da [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 Di seguito vengono descritti gli scenari in cui le applicazioni possono trarre vantaggio dall'accesso a livello di codice ai servizi di replica:  
  
-   Aggiunta di funzionalità di replica a un'applicazione dell'utente finale esistente, ad esempio la sincronizzazione di una sottoscrizione pull quando l'utente fa clic su un pulsante.  
  
-   Creazione di un'interfaccia utente basata sul web per l'amministrazione remota della replica.  
  
-   Creazione di un'interfaccia utente personalizzata che esponga solo un subset delle funzionalità di amministrazione e che possa essere utilizzata per l'amministrazione remota di più topologie di replica da un solo percorso o che combini funzionalità di amministrazione e di sincronizzazione.  
  
-   Miglioramento di uno strumento di monitoraggio esistente mediante l'aggiunta di funzionalità di controllo dello stato di una pubblicazione o di una sottoscrizione o presso il server di distribuzione.  
  
-   Creazione di un'applicazione personalizzata per amministrare o sincronizzare sottoscrizioni di un server di pubblicazione Oracle.  
  
-   Scrittura di regole business personalizzate da eseguire alla sincronizzazione di una sottoscrizione di tipo merge.  
  
-   Generazione di script [!INCLUDE[tsql](../../../includes/tsql-md.md)] che possono essere eseguiti ripetutamente durante la configurazione di nuovi sottoscrittori.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente di controllare a livello di codice gli agenti di replica e di amministrare e monitorare a livello di codice una topologia di replica. Per altre informazioni sulla programmazione della replica, vedere [Concetti di base relativi alla programmazione della replica](replication-programming-concepts.md).  
  
## <a name="in-this-section"></a>In questa sezione  
 [Concetti di base relativi alla programmazione della replica](replication-programming-concepts.md)  
 Descrive i passaggi di pianificazione per lo sviluppo di un'applicazione che utilizza la replica.  
  
 [Replication System Stored Procedures Concepts](replication-system-stored-procedures-concepts.md)  
 Descrive come è possibile utilizzare stored procedure di sistema per fornire l'accesso a livello di codice in una topologia di replica.  
  
 [Concetti di base relativi a RMO (Replication Management Objects)](replication-management-objects-concepts.md)  
 Illustra i concetti di base per l'utilizzo di RMO (Replication Management Objects), ovvero un assembly di codice gestito che incapsula le funzionalità di replica per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Concetti di base relativi ai file eseguibili dell'agente di replica](replication-agent-executables-concepts.md)  
 Descrive l'utilizzo di file eseguibili dell'agente di replica.  
  
 [Guida per sviluppatori: Procedure relative al &#40;replica&#41;](../developer-s-guide-how-to-topics-replication.md)  
 Fornisce un elenco di procedure correlate alla replica.  
  
  
