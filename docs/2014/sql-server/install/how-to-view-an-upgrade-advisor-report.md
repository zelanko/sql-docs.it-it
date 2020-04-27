---
title: 'Procedura: visualizzazione di un report di preparazione aggiornamento | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- viewing reports
- Upgrade Advisor [SQL Server], reports
- SQL Server Upgrade Advisor, reports
- reports [Upgrade Advisor], viewing
ms.assetid: d13b38af-0ac3-4030-83cd-e7d7825dd09f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0ae231e380530f11d4c97a917927ed62e99fb47
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094799"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>Procedura: Visualizzazione di un report di Preparazione aggiornamento
  Preparazione aggiornamento crea report per ogni componente selezionato da analizzare. In questo argomento viene descritto come visualizzare un report di Preparazione aggiornamento dalla pagina iniziale di Preparazione aggiornamento.  
  
> [!IMPORTANT]  
>  Il visualizzatore di report carica file in base ai nomi file standard. Se i file sono stati rinominati, non verranno caricati.  
  
### <a name="to-view-a-report"></a>Per visualizzare un report  
  
1.  Fare clic su **Start**, scegliere **tutti i programmi**, fare **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** clic su, quindi su ** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] preparazione aggiornamento**.  
  
2.  Nella pagina iniziale di preparazione aggiornamento fare clic su **Avvia Visualizzatore report di preparazione aggiornamento**.  
  
3.  Per selezionare un report nel percorso predefinito nel computer:  
  
    1.  Nell'elenco **Server** selezionare un server.  
  
    2.  Nell'elenco **istanza o** componente selezionare una combinazione componente o componente/istanza.  
  
     Per selezionare un report in un altro percorso:  
  
    1.  Fare clic sul collegamento **Apri report** .  
  
    2.  Passare al percorso del report, quindi fare doppio clic sul file XML.  
  
     Preparazione aggiornamento consente di archiviare fino a cinque report dell'analisi precedente come cronologia. Per visualizzare i report, fare clic sulla casella di riepilogo a discesa **report** e selezionare un report. I report vengono elencati in base al valore timestamp che indica la data e l'ora in cui sono stati generati.  
  
     Il report contiene i dettagli seguenti per tutti i problemi rilevati:  
  
    -   **Importanza**, che indica l'importanza della risoluzione del problema.  
  
    -   **Quando correggere**, che indica se è necessario (o) correggere il problema prima o dopo l'aggiornamento a, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]prima o dopo la migrazione dell'applicazione o dei dati o in qualsiasi momento.  
  
    -   Breve descrizione del problema.  
  
4.  Se il report contiene più di 20 elementi, fare clic sulla freccia avanti verde nella parte superiore o inferiore del report per visualizzare il set successivo di elementi. Fare clic sul pulsante indietro verde per visualizzare i 20 elementi precedenti.  
  
5.  Per ordinare il report, fare clic su un'intestazione di colonna.  
  
6.  Per visualizzare i dettagli per un elemento specifico, fare clic su di esso. Verrà visualizzata una descrizione del problema, oltre a opzioni aggiuntive:  
  
    -   Per visualizzare gli oggetti in cui è stato rilevato il problema, fare clic su **Mostra oggetti interessati**.  
  
    -   Per visualizzare la guida per il problema, fare clic su **ulteriori informazioni su questo problema e su come risolverlo**.  
  
    -   Per contrassegnare il problema come risolto, in modo da nascondere il problema quando si visualizza di nuovo il report, selezionare **questo problema è stato risolto**.  
  
> [!NOTE]  
>  Il report può contenere un elemento relativo a problemi non rilevabili, ovvero problemi che non è possibile rilevare o che genererebbero un numero eccessivo di risultati falsi positivi. Fare clic sul collegamento **ulteriori informazioni su questo problema e su come risolverlo** per visualizzare un elenco di problemi non rilevabili per il componente.  
  
## <a name="see-also"></a>Vedi anche  
 [Procedura: esportazione di report](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Procedura: esecuzione dell'analisi guidata di preparazione aggiornamento](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Risoluzione dei problemi di aggiornamento](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Procedure per preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
