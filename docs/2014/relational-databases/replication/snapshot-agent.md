---
title: Agente snapshot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.snapshotagent.f1
helpviewer_keywords:
- Snapshot Agent dialog box
ms.assetid: b715e621-2cd5-4a15-8f58-a341aa8ef5e4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a5f9f869c076365a4c1f10a9ffacbf4a3cbae009
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777553"
---
# <a name="snapshot-agent"></a>agente snapshot
  Nella finestra di dialogo **Agente snapshot** vengono visualizzate informazioni dettagliate sull'agente snapshot, inclusi lo stato, la cronologia, i messaggi informativi e tutti quelli di errore.  
  
## <a name="options"></a>Opzioni  
 Scegliere le sessioni dell'agente snapshot da visualizzare dal menu **Visualizza** e quindi selezionare una specifica sessione nella griglia con etichetta **Sessioni dell'agente snapshot**. Nella griglia con etichetta **Azioni nella sessione selezionata**verranno visualizzate informazioni dettagliate sulla sessione selezionata. Se la sessione selezionata è terminata con un errore, verrà inoltre visualizzata l'area di testo con etichetta **Messaggio o dettagli errore della sessione selezionata** .  
  
 **Visualizza**  
 Consente di selezionare le sessioni dell'agente snapshot da visualizzare.  
  
 **Stato**  
 Stato dell'agente snapshot. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Ripetizione comando non riuscito  
  
-   Non in esecuzione  
  
-   Operazione completata  
  
 **Start Time**  
 Ora di inizio della sessione.  
  
 **Ora fine**  
 Ora di fine della sessione. Se l'agente non è arrestato, questo campo è vuoto.  
  
 **Durata**  
 Periodo di tempo per cui l'agente snapshot è stato eseguito in questa sessione. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e la durata totale della sessione se la sessione dell'agente è terminata.  
  
 **Messaggio di errore**  
 Se una sessione è terminata con un errore, in questo campo verrà visualizzato l'ultimo messaggio di errore registrato dall'agente snapshot. Se una sessione non è terminata con un errore, questo campo è vuoto.  
  
 **Messaggio azione**  
 Tutti i messaggi informativi e di errore registrati dall'agente snapshot durante la sezione selezionata.  
  
 **Ora azione**  
 Ora di esecuzione dell'azione descritta nella colonna **Messaggio azione** .  
  
 **Messaggio o dettagli errore della sessione selezionata**  
 Area visualizzata solo se per la sessione selezionata è visualizzato il valore **Errore** nella colonna **Stato** . In questa area di testo vengono visualizzate informazioni dettagliate sull'errore e viene indicato il comando di cui è stata tentata l'esecuzione quando si è verificato l'errore. Sono inoltre disponibili collegamenti a contenuto aggiuntivo correlato all'errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una pubblicazione &#40;Monitoraggio replica&#41;](monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [Monitoraggio della replica](monitoring-replication.md)   
 [Panoramica degli agenti di replica](agents/replication-agents-overview.md)  
  
  
