---
title: Sottoscrizione, Cronologia server di distribuzione - Sottoscrittore (sottoscrizione transazionale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.disttosub.f1
ms.assetid: 1aad5b82-592e-4907-92f7-b90794175be5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b8d858e8b7ab62ac22902a15159163f8d6d01889
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133513"
---
# <a name="subscription-distributor-to-subscriber-history-transactional-subscription"></a>Sottoscrizione, Cronologia server di distribuzione - Sottoscrittore (Sottoscrizione transazionale)
  Nella scheda **Cronologia server di distribuzione - Sottoscrittore** vengono visualizzate informazioni dettagliate sull'agente di distribuzione, quali lo stato, la cronologia, i messaggi informativi ed eventuali messaggi di errore.  
  
## <a name="options"></a>Opzioni  
 Scegliere le sessioni dell'agente di distribuzione da visualizzare dal menu **Visualizza** e quindi selezionare una sessione specifica nella griglia con etichetta **Sessioni dell'agente di distribuzione**. Nella griglia con etichetta **Azioni nella sessione selezionata**verranno visualizzate informazioni dettagliate sulla sessione selezionata. Se la sessione selezionata è terminata con un errore, verrà inoltre visualizzata l'area di testo con etichetta **Messaggio o dettagli errore della sessione selezionata** .  
  
 **Visualizza**  
 Consente di selezionare le sessioni dell'agente di distribuzione da visualizzare. L'esecuzione dell'agente di distribuzione è in genere continua. Potrebbe pertanto essere presente una sola sessione.  
  
 **Stato**  
 Stato dell'agente di distribuzione. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Operazione completata  
  
-   Nuovo tentativo in corso  
  
-   In esecuzione  
  
 **Start Time**  
 Ora di inizio della sessione.  
  
 **Ora fine**  
 Ora di fine della sessione. Se l'agente non è arrestato, questo campo è vuoto.  
  
 **Durata**  
 Periodo di tempo durante il quale l'agente di distribuzione è stato eseguito in questa sessione. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e la durata totale della sessione se la sessione dell'agente è terminata.  
  
 **Messaggio di errore**  
 Se una sessione è terminata con un errore, in questo campo viene visualizzato l'ultimo messaggio di errore registrato dall'agente di distribuzione. Se una sessione non è terminata con un errore, questo campo è vuoto.  
  
 **Messaggio azione**  
 Tutti i messaggi informativi e i messaggi di errore registrati dall'agente di distribuzione durante la sessione selezionata.  
  
 **Ora azione**  
 Ora di esecuzione dell'azione descritta nella colonna **Messaggio azione** .  
  
 **Messaggio o dettagli errore della sessione selezionata**  
 Area visualizzata solo se per la sessione selezionata è visualizzato il valore **Errore** nella colonna **Stato** . In questa area di testo vengono visualizzate informazioni dettagliate sull'errore e viene indicato il comando di cui è stata tentata l'esecuzione quando si è verificato l'errore. Sono inoltre disponibili collegamenti a contenuto aggiuntivo correlato all'errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md)   
 [Visualizzare informazioni ed eseguire attività con Monitoraggio replica](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitoraggio della replica](monitoring-replication.md)   
 [Panoramica degli agenti di replica](agents/replication-agents-overview.md)  
  
  
