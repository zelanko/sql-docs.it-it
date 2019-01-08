---
title: Sottoscrizione, Cronologia sincronizzazione (sottoscrizione di tipo merge, SQL Server 2000) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.downlevelsynchhistory.f1
ms.assetid: 0a0deab2-1c08-4371-9681-d9403e0236cc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 435b24f8f6d7c9255db3c7d72f78ffe474a85c6e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52821985"
---
# <a name="subscription-synchronization-history-merge-subscription-sql-server-2000"></a>Sottoscrizione, Cronologia sincronizzazione (Sottoscrizione di tipo merge, SQL Server 2000)
  Nella scheda **Cronologia sincronizzazione** vengono visualizzate informazioni dettagliate sull'agente di merge, fra cui lo stato, la cronologia, i messaggi informativi e tutti gli eventuali messaggi di errore.  
  
## <a name="options"></a>Opzioni  
 Scegliere le sessioni dell'agente di merge da visualizzare dal menu **Visualizza** e quindi selezionare una sessione specifica nella griglia con l'etichetta **Sessioni dell'agente di merge**. Nella griglia con etichetta **Azioni nella sessione selezionata**verranno visualizzate informazioni dettagliate sulla sessione selezionata. Se la sessione selezionata è terminata con un errore, verrà inoltre visualizzata l'area di testo con etichetta **Messaggio o dettagli errore della sessione selezionata** .  
  
 **Visualizza**  
 Consente di selezionare l'agente di merge da visualizzare. L'agente di merge è in genere in esecuzione continua e potrebbe pertanto essere presente un'unica sessione da visualizzare.  
  
 **Stato**  
 Stato dell'agente di merge. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Operazione completata  
  
-   Nuovo tentativo in corso  
  
-   In esecuzione  
  
 **Start Time**  
 Ora di inizio della sessione.  
  
 **Ora fine**  
 Ora di fine della sessione. Se l'agente non è arrestato, questo campo è vuoto.  
  
 **Durata**  
 Quantità di tempo di esecuzione dell'agente di merge nella sessione. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e la durata totale della sessione se la sessione dell'agente è terminata.  
  
 **Messaggio di errore**  
 Se una sessione è terminata con un errore, in questo campo viene visualizzato l'ultimo messaggio di errore registrato dall'agente di merge. Se una sessione non è terminata con un errore, questo campo è vuoto.  
  
 **Messaggio azione**  
 Tutti i messaggi informativi e di errore registrati dall'agente di merge durante la sessione selezionata.  
  
 **Ora azione**  
 Ora di esecuzione dell'azione descritta nella colonna **Messaggio azione** .  
  
 **Messaggio o dettagli errore della sessione selezionata**  
 Area visualizzata solo se per la sessione selezionata è visualizzato il valore **Errore** nella colonna **Stato** . In questa area di testo vengono visualizzate informazioni dettagliate sull'errore e viene indicato il comando di cui è stata tentata l'esecuzione quando si è verificato l'errore. Sono inoltre disponibili collegamenti a contenuto aggiuntivo correlato all'errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una sottoscrizione &#40;Monitoraggio replica&#41;](monitor/view-information-and-perform-tasks-for-subscription-agents.md)   
 [Monitoraggio della replica](monitoring-replication.md)   
 [Panoramica degli agenti di replica](agents/replication-agents-overview.md)  
  
  
