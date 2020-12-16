---
title: Tipi di replica | Microsoft Docs
description: Informazioni sui diversi tipi di replica resi disponibili da SQL Server per l'uso in applicazioni distribuite.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], types
ms.assetid: c1655e8d-d14c-455a-a7f9-9d2f43e88ab4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: a1f72eeaa2ffff2db3e536eec6f1aa317a2cb45c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468702"
---
# <a name="types-of-replication"></a>Tipi di replica
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre i tipi di replica seguenti, utilizzabili nelle applicazioni distribuite:  

| **Tipo** | **Descrizione** |
|:-------- | :-------------- |
| [Replica transazionale](transactional/transactional-replication.md)| Le modifiche nel server di pubblicazione vengono recapitate al Sottoscrittore nel momento in cui si verificano (quasi in tempo reale). Le modifiche ai dati vengono applicate al Sottoscrittore nello stesso ordine e entro gli stessi limiti della transazione con cui vengono eseguite nel server di pubblicazione. | 
| [Replica di tipo merge](merge/merge-replication.md) | I dati possono essere modificati sia nel server di pubblicazione che nel Sottoscrittore e vengono rilevati con i trigger. Al momento della connessione alla rete il Sottoscrittore esegue la sincronizzazione con il server di pubblicazione e scambia con esso le righe modificate dopo l'ultima sincronizzazione. | 
| [Replica snapshot](snapshot-replication.md) | Applica uno snapshot dal server di pubblicazione al Sottoscrittore, che distribuisce i dati così come appaiono in uno determinato momento e non prevede il monitoraggio degli aggiornamenti ai dati. Quando viene eseguita la sincronizzazione, viene generato e inviato ai Sottoscrittori l'intero snapshot.| 
| [Peer-to-peer](transactional/peer-to-peer-transactional-replication.md) | Compilata sulle basi della replica transazionale, la replica peer-to-peer propaga quasi in tempo reale modifiche coerenti dal punto di vista transazionale tra più istanze del server. | 
| [Bidirezionale](transactional/bidirectional-transactional-replication.md)| La replica transazionale bidirezionale è una topologia di replica transazionale specifica che consente lo scambio reciproco di modifiche tra due server: ogni server pubblica i dati e successivamente esegue la sottoscrizione di una pubblicazione con gli stessi dati dell'altro server. | 
| [Sottoscrizioni aggiornabili](transactional/updatable-subscriptions-for-transactional-replication.md) | Sulla base della replica transazionale, quando i dati vengono aggiornati in un Sottoscrittore per una sottoscrizione aggiornabile, vengono prima propagati al server di pubblicazione e quindi propagati agli altri Sottoscrittori. | 
  
 
Il tipo di replica selezionato per un'applicazione dipende da numerosi fattori, tra cui l'ambiente fisico di replica, il tipo e la quantità di dati da replicare e l'eventuale presenza di dati aggiornati nel Sottoscrittore. L'ambiente fisico include il numero e la posizione dei computer coinvolti nella replica, nonché se si tratti di computer client (workstation, computer portatili o dispositivi palmari) o server.  
  
Ogni tipo di replica ha in genere inizio con una sincronizzazione degli oggetti pubblicati tra server di pubblicazione e Sottoscrittori. Questa sincronizzazione iniziale può essere eseguita dalla replica con uno *snapshot*, ovvero una copia di tutti gli oggetti e i dati specificati da una pubblicazione. Dopo la creazione, lo snapshot viene recapitato ai Sottoscrittori. Per alcune applicazioni, è sufficiente la replica snapshot. Per altri tipi di applicazioni, è importante che esista un flusso incrementale nel tempo delle successive modifiche di dati al Sottoscrittore. Alcune applicazioni richiedono inoltre il flusso delle modifiche dal Sottoscrittore al server di pubblicazione. La replica transazionale e la replica di tipo merge offrono opzioni per questi tipi di applicazioni.  
  
 
## <a name="see-also"></a>Vedere anche  
 [Panoramica degli agenti di replica](../../relational-databases/replication/agents/replication-agents-overview.md)
  
  
