---
title: Inizializzazione nuovi peer (replica peer-to-peer) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.p2pwizard.init.f1
ms.assetid: 050c00e1-78bd-4d9c-affe-40e22feb4d94
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5fae974b7ec8378db7874a7a4c173953b1983595
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020156"
---
# <a name="new-peer-initialization-peer-to-peer-replication"></a>Inizializzazione nuovi peer (replica peer-to-peer)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La pagina **Inizializzazione nuovi peer** consente di specificare la modalità di inizializzazione dei database peer. I peer devono essere inizializzati prima di completare la procedura guidata. I peer possono essere inizializzati manualmente oppure utilizzando la funzionalità **initialize with backup** fornita dalla replica transazionale. La replica transazionale peer-to-peer non supporta l'inizializzazione dei peer tramite uno snapshot. Se peer diversi devono essere inizializzati utilizzando metodi diversi, è necessario aggiungere i peer separatamente eseguendo più volte la procedura guidata.  
  
## <a name="options"></a>Opzioni  
 **Specificare il tipo di inizializzazione dei nuovi database peer**  
 È necessario che lo schema e i dati relativi a tutti gli oggetti pubblicati siano presenti in ogni peer. Selezionare una delle opzioni seguenti:  
  
-   Selezionare la prima opzione nel caso in cui lo schema relativo agli oggetti pubblicati sia stato creato manualmente oppure sia stato ripristinato un backup e non siano state apportate modifiche ai dati nel primo database di pubblicazione dal momento dell'esecuzione del backup. Se lo schema è stato creato manualmente, è necessario verificare che tutti i dati necessari siano presenti in ogni peer. Questa opzione corrisponde al valore **replication support only** della proprietà di sottoscrizione **sync_type**.  
  
-   Selezionare la seconda opzione nel caso in cui sia stato ripristinato un backup e siano state apportate modifiche ai dati nel primo database di pubblicazione dal momento dell'esecuzione del backup. È necessario quindi che la replica recapiti le modifiche non incluse nel backup del primo database di pubblicazione. Questa opzione corrisponde al valore **initialize with backup** della proprietà di sottoscrizione **sync_type**.  
  
     Quando viene abilitata una pubblicazione per la replica peer-to-peer, viene impostata la proprietà di pubblicazione **allow_initialize_from_backup** . La replica inizierà immediatamente a rilevare le modifiche nel primo database di pubblicazione. Queste modifiche possono pertanto essere recapitate a un database ripristinato in uno o più peer se l'opzione **initialize with backup** è selezionata. Fare clic sul pulsante **Sfoglia** per individuare il backup utilizzato. Tramite la replica, verrà letto il numero di sequenza del file di log (LSN) dal backup. Tutte le modifiche apportate al primo database di pubblicazione a cui è associato un numero di sequenza del file di log superiore verranno recapitate a tutti i peer.  
  
     Questa opzione potrebbe non essere disponibile se si sta eseguendo la creazione o l'aggiunta in una topologia che include [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Nella tabella seguente viene indicato se l'opzione è disponibile quando si aggiunge un nodo a una topologia esistente.  
  
    |Nuovo nodo|Primo nodo|Nodi aggiuntivi|Opzione|  
    |--------------|----------------|----------------------|------------|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Disabilitata|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|None|Disabilitata|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Disabilitata|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|None|Abilitata|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|None|Abilitata|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|Abilitata|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|None|Abilitata|  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare una topologia peer-to-peer &#40;programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
