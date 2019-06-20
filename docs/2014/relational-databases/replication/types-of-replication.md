---
title: Tipi di replica | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], types
ms.assetid: c1655e8d-d14c-455a-a7f9-9d2f43e88ab4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4dd5d28bb3b40417ab9c16b957b48db04f44599f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63255449"
---
# <a name="types-of-replication"></a>Tipi di replica
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre i tipi di replica seguenti, utilizzabili nelle applicazioni distribuite:  
  
-   Replica transazionale. Per altre informazioni, vedere [Replica transazionale](transactional/transactional-replication.md).  
  
-   Replica di tipo merge. Per altre informazioni, vedere [Replica di tipo merge](merge/merge-replication.md).  
  
-   Replica snapshot. Per altre informazioni, vedere [Replica snapshot](snapshot-replication.md).  
  
 Il tipo di replica selezionato per un'applicazione dipende da numerosi fattori, tra cui l'ambiente fisico di replica, il tipo e la quantità di dati da replicare e l'eventuale presenza di dati aggiornati nel Sottoscrittore. L'ambiente fisico include il numero e la posizione dei computer coinvolti nella replica, nonché se si tratti di computer client (workstation, computer portatili o dispositivi palmari) o server.  
  
 Ogni tipo di replica ha in genere inizio con una sincronizzazione degli oggetti pubblicati tra server di pubblicazione e Sottoscrittori. Questa sincronizzazione iniziale può essere eseguita dalla replica con uno *snapshot*, ovvero una copia di tutti gli oggetti e i dati specificati da una pubblicazione. Dopo la creazione, lo snapshot viene recapitato ai Sottoscrittori. Per alcune applicazioni, è sufficiente la replica snapshot. Per altri tipi di applicazioni, è importante che esista un flusso incrementale nel tempo delle successive modifiche di dati al Sottoscrittore. Alcune applicazioni richiedono inoltre il flusso delle modifiche dal Sottoscrittore al server di pubblicazione. La replica transazionale e la replica di tipo merge offrono opzioni per questi tipi di applicazioni.  
  
 Le modifiche di dati non vengono rilevate per la replica snapshot. Ogni volta che viene applicato uno snapshot, vengono completamente sovrascritti i dati esistenti. La replica transazionale rileva le modifiche tramite il log delle transazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mentre la replica di tipo merge utilizza a tale scopo trigger e tabelle di metadati.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica degli agenti di replica](agents/replication-agents-overview.md)  
  
  
