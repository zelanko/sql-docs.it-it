---
title: Istanza di Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ed71e8c4-e013-4bf2-8b6c-1e833ff2a41d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0152594c213196860e80ff5d5267356977404b7d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62771191"
---
# <a name="the-oracle-cdc-instance"></a>Istanza di Oracle CDC
  L'istanza di Oracle CDC è un processo creato dal servizio Oracle CDC per elaborare le modifiche acquisite da un solo database di origine Oracle. Tramite l'istanza di Oracle CDC viene recuperata la configurazione dalla tabella **cdc.xdbcdc_config** e viene gestito lo stato nella tabella **cdc.xdbcdc_state** . Queste tabelle fanno parte del database CDC che definisce l'istanza di Oracle CDC. Per ulteriori informazioni sul database e le tabelle xdbcdc, vedere [The CDC Databases](the-oracle-cdc-service.md).  
  
 Di seguito vengono descritte le attività eseguite dall'istanza di Oracle CDC:  
  
-   **Gestione della verifica dell'avvio del servizio**: all'avvio, tramite l'istanza di CDC viene caricata la configurazione dalla tabella **xdbcdc_config** e viene eseguita una serie di verifiche dello stato per controllare che lo stato persistente dell'istanza di CDC sia coerente e che sia possibile avviare l'elaborazione delle modifiche.  
  
-   **Preparazione per l'acquisizione delle modifiche**: al completamento della verifica, tramite l'istanza di Oracle CDC vengono analizzate tutte le istanze di acquisizione attualmente definite e vengono preparate le query Oracle LogMiner e altre strutture di supporto necessarie per l'acquisizione delle modifiche. Inoltre, viene ricaricato lo stato di acquisizione interno salvato all'ultima esecuzione dell'istanza di Oracle CDC.  
  
-   **Acquisizione delle modifiche da Oracle**: tramite l'istanza di Oracle CDC le modifiche da Oracle vengono riunite in pool mediante la struttura Oracle LogMiner e ordinate in base al commit della transazione, viene modificata l'ora di una transazione, quindi le modifiche vengono scritte nelle tabelle delle modifiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel database CDC.  
  
-   **Gestione dell'arresto del servizio**: il ciclo di vita dell'istanza di Oracle CDC viene gestito dal servizio Oracle CDC. Quando è richiesto l'arresto dell'istanza di Oracle CDC, vengono effettuate le attività seguenti:  
  
    -   Viene arrestata la lettura del log delle transazioni Oracle.  
  
    -   Viene arrestata la scrittura delle transazioni Oracle completate nel database CDC.  
  
    -   Viene attesa la fine della scrittura della transazione corrente nel database CDC per un massimo di 30 secondi, se necessario. Se trascorrono più di 30 secondi, la scrittura viene annullata e viene eseguito il rollback della transazione (da tentare nuovamente al riavvio dell'istanza di CDC).  
  
    -   In un thread separato, viene scritto il numero più alto possibile di record memorizzati nella cache nella tabella delle transazioni gestite temporaneamente per un massimo di 30 secondi (dalla transazione meno recente alla più recente), quindi viene aggiornata la tabella **xdbcdc_state** e viene eseguito il commit di tutte le modifiche.  
  
-   **Gestione delle modifiche della configurazione**: viene inviata una notifica all'istanza di Oracle CDC relativamente alle modifiche della configurazione dal servizio CDC o mediante il rilevamento di una nuova versione nella tabella **cdc.xdbcdc_config** . La maggior parte delle modifiche non richiede il riavvio dell'istanza di Oracle CDC (ad esempio l'aggiunta o la rimozione delle istanze di acquisizione). Alcune modifiche, tuttavia, ad esempio la modifica della stringa di connessione Oracle o delle credenziali di accesso richiedono il riavvio dell'istanza di CDC.  
  
-   **Gestione del recupero**: all'avvio di un'istanza di Oracle CDC, il relativo stato interno viene ripristinato dalle tabelle **xdbcdc_state** e **xdbcdc_staged_transactions** . Una volta ripristinato lo stato, il processo dell'istanza di CDC prosegue nel modo consueto.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione degli errori](error-handling.md)  
  
  
