---
title: Altri problemi di aggiornamento replica | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- system tables [SQL Server], replication
- passwords [SQL Server replication]
- versions [SQL Server replication]
- connections [SQL Server replication]
- scripts [SQL Server replication]
- ActiveX controls [SQL Server replication]
ms.assetid: 8a5e74be-4992-4f17-b20c-c3dce8f49329
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5ffde063d94f0e08ea0e82e6b5998a6d23cfaac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62473182"
---
# <a name="other-replication-upgrade-issues"></a>Altri problemi di aggiornamento della replica
  In questo argomento vengono analizzati alcuni problemi relativi all'aggiornamento che non sono segnalati da Preparazione aggiornamento.  
  
## <a name="versions-supported"></a>Versioni supportate  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] supporta l'aggiornamento di database replicati da versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Durante l'aggiornamento di un nodo, non è necessario arrestare l'attività eseguita su altri nodi. Verificare che vengano osservate le regole relative alle versioni supportate in una topologia.  
  
 È possibile eseguire funzionalità di replica tra versioni diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anche se tali funzionalità sono in genere limitate a quelle supportate dalla versione meno recente utilizzata.  
  
> [!NOTE]  
>  Poiché in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il formato di archiviazione su disco è lo stesso in ambienti a 64 bit e a 32 bit, in una topologia di replica possono essere presenti istanze del server eseguite in un ambiente a 32 bit e istanze del server eseguite in un ambiente a 64 bit.  
  
 Per tutti i tipi di replica, la versione del server di distribuzione non deve essere precedente a quella del server di pubblicazione. In molti casi l'istanza del server di distribuzione è la stessa di quella del server di pubblicazione.  
  
 In caso di replica transazionale, la versione di un Sottoscrittore di una pubblicazione transazionale è limitata a un intervallo di due versioni in base alla versione del server di pubblicazione.  
  
 In caso di replica di tipo merge, è possibile utilizzare qualsiasi versione del Sottoscrittore di una pubblicazione di tipo merge, purché non sia successiva a quella del server di pubblicazione.  
  
## <a name="merge-replication-batches-changes"></a>Modifiche eseguite in batch della replica di tipo merge  
 Le modifiche apportate dall'agente di merge vengono eseguite in batch per migliorare le prestazioni. Di conseguenza, all'interno di una singola istruzione è possibile inserire, aggiornare o eliminare più righe. Se nei database di pubblicazione o di sottoscrizione sono presenti tabelle pubblicate che contengono trigger, verificare che i trigger siano in grado di gestire gli inserimenti, gli aggiornamenti e le eliminazioni di più righe. Per ulteriori informazioni, vedere "Considerazioni sulle istruzioni che interessano più righe per i trigger DML" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="activex-control-changes"></a>Modifiche ai controlli ActiveX  
 Ai controlli ActiveX della replica sono state apportate le seguenti modifiche:  
  
-   Tutti i controlli ActiveX sono contrassegnati come non sicuri per la generazione di script e l'inizializzazione.  
  
-   Il controllo ActiveX snapshot è stato eliminato. È possibile creare e gestire snapshot utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oppure a livello di programmazione mediante stored procedure di replica. Per altre informazioni, vedere gli argomenti "procedura: Creare e applicare lo Snapshot iniziale ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) "e" procedura: Creare lo Snapshot iniziale (programmazione Transact-SQL della replica) "in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
-   I controlli ActiveX distribuzione e ActiveX merge sono stati deprecati. Una funzionalità analoga viene fornita per applicazioni del codice gestito da oggetti RMO (Replication Management Objects). Per ulteriori informazioni, vedere l'argomento relativo alla sincronizzazione delle sottoscrizioni (programmazione RMO) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento della replica](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  
