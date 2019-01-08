---
title: 'Esercitazione: Replica continua dei dati tra server con connessione | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 32b97d456c42eab89511d8f5a9d1924914ea81ca
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52753923"
---
# <a name="tutorial-replicating-data-between-continuously-connected-servers"></a>Esercitazione: Replica di dati tra server con connessione continua
  La replica è una buona soluzione al problema legato al trasferimento dei dati tra server con connessione continua. Le procedure guidate relative alla replica consentono di eseguire in modo semplificato i passaggi necessari per configurare e amministrare una topologia di replica. In questa esercitazione viene descritto come configurare una topologia di replica per server con connessione continua.  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 In questa esercitazione viene descritto come pubblicare dati da un database all'altro mediante la replica transazionale. Nella prima lezione verranno descritte le procedure per la creazione di una pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Nelle lezioni seguenti verranno descritte le procedure per creare e convalidare una sottoscrizione e per misurare la latenza.  
  
## <a name="requirements"></a>Requisiti  
 Questa esercitazione è destinata agli utenti esperti nelle operazioni di database di base ma con una limitata conoscenza della replica. Per eseguire questa esercitazione è necessario avere completato l'esercitazione precedente [Preparazione del server per la replica](tutorial-preparing-the-server-for-replication.md).  
  
 Per utilizzare l'esercitazione è necessario che nel sistema siano installati i componenti seguenti:  
  
-   Nel server di pubblicazione (origine):  
  
    -   Qualsiasi edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad eccezione di Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) o [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Questa edizioni non possono fungere da server di pubblicazione per la replica.  
  
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] database di esempio. Per una maggiore sicurezza, i database di esempio non vengono installati per impostazione predefinita.  
  
-   Sottoscrittore (destinazione):  
  
    -   Qualsiasi edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad eccezione di [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] non può essere un Sottoscrittore nella replica transazionale.  
  
    > [!NOTE]  
    >  Per impostazione predefinita la replica non è installata in [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] .  
  
> [!NOTE]  
>  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]è necessario connettersi al server di pubblicazione e al Sottoscrittore mediante un account di accesso membro del ruolo fisso del server **sysadmin** .  
  
 **Tempo stimato per completare questa esercitazione: 30 minuti.**  
  
## <a name="lessons-in-this-tutorial"></a>Lezioni dell'esercitazione  
  
-   [Lezione 1: Pubblicazione dei dati tramite la replica transazionale](lesson-1-publishing-data-using-transactional-replication.md)  
  
-   [Lezione 2: Creazione di una sottoscrizione per una pubblicazione transazionale](lesson-2-creating-a-subscription-to-the-transactional-publication.md)  
  
-   [Lezione 3: Convalida della sottoscrizione e misurazione della latenza](lesson-3-validating-the-subscription-and-measuring-latency.md)  
  
 [Avviare l'esercitazione](transactional/transactional-replication.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti di base relativi alla programmazione della replica](concepts/replication-programming-concepts.md)  
  
  
