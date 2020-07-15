---
title: Documentazione per gli sviluppatori di replica | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- developer's guide [SQL Server replication]
- programming [SQL Server replication]
- replication [SQL Server], development
ms.assetid: 7ee134ae-1cab-4a35-8017-8ac6d8fc64b6
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: aab3d0528452b5e77746307840899fc193a00ccc
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2020
ms.locfileid: "86158949"
---
# <a name="replication-developer-documentation"></a>Documentazione per gli sviluppatori di replica
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/applies-to-version/sql-asdbmi.md)]

  La possibilità da configurare, gestire e monitorare a livello di codice una topologia di replica consente di semplificare le attività di replica ripetute e di migliorare l'esperienza utente per le applicazioni basate sulla replica. Mediante la programmazione della replica, è possibile offrire funzionalità di replica personalizzate agli utenti finali, senza che sia necessario conoscere le stored procedure di replica e i file eseguibili degli agenti di replica o utilizzare l'interfaccia di replica implementata da [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 Di seguito vengono descritti gli scenari in cui le applicazioni possono trarre vantaggio dall'accesso a livello di codice ai servizi di replica:  
  
-   Aggiunta di funzionalità di replica a un'applicazione dell'utente finale esistente, ad esempio la sincronizzazione di una sottoscrizione pull quando l'utente fa clic su un pulsante.  
  
-   Creazione di un'interfaccia utente basata sul web per l'amministrazione remota della replica.  
  
-   Creazione di un'interfaccia utente personalizzata che esponga solo un subset delle funzionalità di amministrazione e che possa essere utilizzata per l'amministrazione remota di più topologie di replica da un solo percorso o che combini funzionalità di amministrazione e di sincronizzazione.  
  
-   Miglioramento di uno strumento di monitoraggio esistente mediante l'aggiunta di funzionalità di controllo dello stato di una pubblicazione o di una sottoscrizione o presso il server di distribuzione.  
  
-   Creazione di un'applicazione personalizzata per amministrare o sincronizzare sottoscrizioni di un server di pubblicazione Oracle.  
  
-   Scrittura di regole business personalizzate da eseguire alla sincronizzazione di una sottoscrizione di tipo merge.  
  
-   Generazione di script [!INCLUDE[tsql](../../../includes/tsql-md.md)] che possono essere eseguiti ripetutamente durante la configurazione di nuovi sottoscrittori.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente di controllare a livello di codice gli agenti di replica e di amministrare e monitorare a livello di codice una topologia di replica. Per altre informazioni sulla programmazione della replica, vedere [Concetti di base relativi alla programmazione della replica](../../../relational-databases/replication/concepts/replication-programming-concepts.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Concetti di base relativi alla programmazione della replica](../../../relational-databases/replication/concepts/replication-programming-concepts.md)  
 Descrive i passaggi di pianificazione per lo sviluppo di un'applicazione che utilizza la replica.  
  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
 Descrive come è possibile utilizzare stored procedure di sistema per fornire l'accesso a livello di codice in una topologia di replica.  
  
 [Concetti di base relativi a RMO (Replication Management Objects)](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
 Illustra i concetti di base per l'utilizzo di RMO (Replication Management Objects), ovvero un assembly di codice gestito che incapsula le funzionalità di replica per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
 Descrive l'utilizzo di file eseguibili dell'agente di replica.  
  
  
  
