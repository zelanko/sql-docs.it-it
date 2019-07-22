---
title: Sottoscrizione, Cronologia sincronizzazione | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.synchhistory.f1
- sql13.rep.monitor.subscription.downlevelsynchhistory.f1
ms.assetid: 85f666f6-14ee-4f19-b385-e5cc508aabe4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9e6c98a6aab879789e73dcab8ce16b53a8b02549
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002700"
---
# <a name="subscription-synchronization-history"></a>Sottoscrizione, Cronologia sincronizzazione
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La scheda **Cronologia sincronizzazione** visualizza informazioni dettagliate sull'agente di merge, tra cui lo stato, le statistiche degli articoli, la cronologia, i messaggi informativi e gli eventuali messaggi di errore.  
  
## <a name="options"></a>Opzioni  
 Scegliere le sessioni dell'agente di merge da visualizzare dal menu **Visualizza** e quindi selezionare una sessione specifica nella griglia con l'etichetta **Sessioni dell'agente di merge**. Nella griglia con l'etichetta **Articoli elaborati nella sessione selezionata**vengono visualizzate informazioni dettagliate sulla sessione.  
  
 **Visualizza**  
 Consente di selezionare l'agente di merge da visualizzare.  
  
 **Stato**  
 Stato dell'agente di merge al termine della sessione. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Completato  
  
-   Nuovo tentativo in corso  
  
-   In esecuzione  
  
 **Start Time**  
 Ora di inizio della sessione.  
  
 **Ora fine**  
 Ora di fine della sessione. Se l'agente non è arrestato, questo campo è vuoto.  
  
 **Durata**  
 Quantità di tempo di esecuzione dell'agente di merge in una sessione. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e la durata totale se l'agente è stato eseguito in precedenza.  
  
 **Comandi caricati**  
 Numero di righe caricate durante la sessione dell'agente di merge.  
  
 **Comandi scaricati**  
 Numero di righe scaricate durante la sessione dell'agente di merge.  
  
 **Messaggio di errore**  
 Se una sessione è terminata con un errore, in questo campo viene visualizzato l'ultimo messaggio di errore registrato dall'agente di merge. Se una sessione non è terminata con un errore, questo campo è vuoto.  
  
 **Articolo**  
 Il nome di ogni articolo della pubblicazione e le fasi di elaborazione seguenti per l'intera pubblicazione:  
  
-   **Inizializzazione**. Si riferisce all'avvio dell'agente di merge e non all'inizializzazione di una sottoscrizione, che invece implica l'applicazione di uno snapshot.  
  
-   **Modifiche dello schema e inserimenti bulk**.  
  
-   **Carica modifiche nel server di pubblicazione**.  
  
-   **Download modifiche nel Sottoscrittore**.  
  
 Le fasi sono incluse in modo che nella griglia sia possibile visualizzare la quantità di tempo e la percentuale della durata totale riferite a ogni fase della sessione selezionata.  
  
 **% del totale**  
 Percentuale del tempo di elaborazione totale riferita a ogni fase della sessione selezionata.  
  
 **Durata**  
 Quantità di tempo utilizzata per ogni fase di elaborazione. Il valore di durata rappresenta il tempo trascorso se l'agente di merge è attualmente in esecuzione per la sessione e la durata totale se l'agente di merge è stato eseguito in precedenza.  
  
 **Inserts**  
 Numero di righe inserite nella fase specifica della sessione selezionata.  
  
 **Aggiornamenti**  
 Numero di righe aggiornate nella fase specifica della sessione selezionata.  
  
 **Eliminazioni**  
 Numero di righe eliminate nella fase specifica della sessione selezionata.  
  
 **Conflitti**  
 Numero di conflitti nella sessione selezionata.  
  
 **Modifiche dello schema**  
 Numero di modifiche dello schema nella sessione selezionata. Le modifiche dello schema possono dipendere da modifiche dello schema apportate al database della pubblicazione, dall'aggiunta o eliminazione di articoli e da modifiche delle proprietà dell'articolo o della pubblicazione.  
  
 **Ultimo messaggio della sessione selezionata**  
 In quest'area di testo viene visualizzato l'ultimo messaggio della sessione selezionata. Se si è verificato un errore, vengono visualizzate informazioni dettagliate sull'errore e il comando di cui si è tentata l'esecuzione al momento dell'errore. Sono inoltre disponibili collegamenti a contenuto aggiuntivo correlato all'errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Panoramica degli agenti di replica](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
