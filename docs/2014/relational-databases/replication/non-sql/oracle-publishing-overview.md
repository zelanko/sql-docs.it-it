---
title: Panoramica della pubblicazione Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], Oracle publishing
- snapshot replication [SQL Server], Oracle publishing
- Oracle publishing [SQL Server replication]
- transactional replication, Oracle publishing
- Oracle publishing [SQL Server replication], about Oracle publishing
ms.assetid: 2e013259-0022-4897-a08d-5f8deb880fa8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 558ee09eeb4419bc354ff3ade9d6586877246b33
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63022252"
---
# <a name="oracle-publishing-overview"></a>Panoramica della pubblicazione Oracle
  Con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] è possibile includere server di pubblicazione Oracle nella topologia di replica, a partire da Oracle versione 9i. I server di pubblicazione possono essere distribuiti su qualsiasi hardware e sistema operativo supportato da Oracle. La funzionalità è compilata sulla base del consolidato meccanismo della replica snapshot e della replica transazionale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ed è in grado di offrire prestazioni e facilità d'uso analoghe.  
  
 La pubblicazione Oracle è deprecata. La replica eterogenea a Sottoscrittori non SQL Server è deprecata. Per spostare dati, creare soluzioni utilizzando Change Data Capture e [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="snapshot-replication-for-oracle"></a>Replica snapshot per Oracle  
 Le pubblicazioni snapshot Oracle vengono implementate in maniera analoga alle pubblicazioni snapshot di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Quando l'agente snapshot viene eseguito per una pubblicazione Oracle, si connette al server di pubblicazione Oracle ed elabora ogni tabella della pubblicazione. Durante l'elaborazione di ogni tabella, l'agente recupera le righe della tabella e crea script dello schema, i quali vengono archiviati nella condivisione snapshot della pubblicazione. L'intero set di dati viene creato ogni volta che l'agente snapshot viene eseguito, quindi i trigger per il rilevamento delle modifiche non vengono aggiunti alle tabelle Oracle, come avviene nella replica transazionale. La replica snapshot rappresenta una soluzione pratica per eseguire la migrazione dei dati con un impatto minimo sul sistema di pubblicazione.  
  
## <a name="transactional-replication-for-oracle"></a>Replica transazionale per Oracle  
 Le pubblicazioni transazionali Oracle vengono implementate tramite l'architettura di pubblicazione transazionale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Le modifiche vengono tuttavia rilevate tramite una combinazione dei trigger di database nel database Oracle e dell'agente di lettura log. I Sottoscrittori di una pubblicazione transazionale Oracle vengono inizializzati automaticamente tramite la replica snapshot, mentre le modifiche successive vengono rilevate e recapitate progressivamente ai Sottoscrittori tramite l'agente di lettura log.  
  
 Quando viene creata una pubblicazione Oracle, vengono creati trigger e tabelle di rilevamento per ogni tabella pubblicata nel database Oracle. Se vengono apportate modifiche ai dati nelle tabelle pubblicate, i trigger del database associati alle tabelle vengono attivati e inseriscono informazioni nelle tabelle di rilevamento della replica per ogni riga modificata. L'agente di lettura log sul server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sposta le informazioni relative alla modifica dei dati dalle tabelle di rilevamento al database di distribuzione sul server di distribuzione. Infine, l'agente di distribuzione sposta le modifiche dal server di distribuzione ai Sottoscrittori, in modo analogo alla replica transazionale standard.  
  
## <a name="see-also"></a>Vedi anche  
 [Configurare un server di pubblicazione Oracle](configure-an-oracle-publisher.md)   
 [Glossario dei termini per la pubblicazione Oracle](glossary-of-terms-for-oracle-publishing.md)   
 [Replica di database eterogenei](heterogeneous-database-replication.md)  
  
  
