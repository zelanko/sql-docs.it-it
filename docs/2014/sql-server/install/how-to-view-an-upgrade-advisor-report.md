---
title: 'Procedura: Visualizzare un Report di preparazione aggiornamento | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
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
ms.openlocfilehash: 90b9ca2879897bb427981e92d610a7f09916c68e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294546"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>Procedura: Visualizzare un report di Gestione spazio aggiornamenti
  Preparazione aggiornamento crea report per ogni componente selezionato da analizzare. In questo argomento viene descritto come visualizzare un report di Preparazione aggiornamento dalla pagina iniziale di Preparazione aggiornamento.  
  
> [!IMPORTANT]  
>  Il visualizzatore di report carica file in base ai nomi file standard. Se i file sono stati rinominati, non verranno caricati.  
  
### <a name="to-view-a-report"></a>Per visualizzare un report  
  
1.  Fare clic su **avviare**, fare clic su **tutti i programmi**, fare clic su **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**, quindi fare clic su  **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Upgrade Advisor**.  
  
2.  Nella pagina iniziale di preparazione aggiornamento, fare clic su **avviare Visualizzatore Report Preparazione aggiornamento**.  
  
3.  Per selezionare un report nel percorso predefinito nel computer:  
  
    1.  Nel **Server** elencare, selezionare un server.  
  
    2.  Nel **istanza o componente** elencare, selezionare una combinazione componente/istanza o componente.  
  
     Per selezionare un report in un altro percorso:  
  
    1.  Scegliere il **Apri Report** collegamento.  
  
    2.  Passare al percorso del report, quindi fare doppio clic sul file XML.  
  
     Preparazione aggiornamento consente di archiviare fino a cinque report dell'analisi precedente come cronologia. Per visualizzare questi report, scegliere il **Report** casella di riepilogo a discesa e selezionare un report. I report vengono elencati in base al valore timestamp che indica la data e l'ora in cui sono stati generati.  
  
     Il report contiene i dettagli seguenti per tutti i problemi rilevati:  
  
    -   **Importanza**, che indica quanto sia importante per risolvere il problema.  
  
    -   **Quando correggere**, che indica se è consigliabile (o necessario) risolvere il problema prima o dopo l'aggiornamento a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], prima o dopo la migrazione di applicazioni o i dati, o in qualsiasi momento.  
  
    -   Breve descrizione del problema.  
  
4.  Se il report contiene più di 20 elementi, fare clic sulla freccia avanti verde nella parte superiore o inferiore del report per visualizzare il set successivo di elementi. Fare clic sul pulsante indietro verde per visualizzare i 20 elementi precedenti.  
  
5.  Per ordinare il report, fare clic su un'intestazione di colonna.  
  
6.  Per visualizzare i dettagli per un elemento specifico, fare clic su di esso. Verrà visualizzata una descrizione del problema, oltre a opzioni aggiuntive:  
  
    -   Per visualizzare gli oggetti in cui è stato trovato questo problema, fare clic su **Show oggetti interessati**.  
  
    -   Per visualizzare la Guida per il problema, fare clic su **ulteriori informazioni su questo problema e su come risolvere il problema**.  
  
    -   Per contrassegnare il problema come risolto, che nasconde il problema quando si visualizza il report anche in questo caso, selezionare **questo problema è stato risolto**.  
  
> [!NOTE]  
>  Il report può contenere un elemento relativo a problemi non rilevabili, ovvero problemi che non è possibile rilevare o che genererebbero un numero eccessivo di risultati falsi positivi. Scegliere il **ulteriori informazioni su questo problema e su come risolvere il problema** collegamento per visualizzare un elenco di problemi non rilevabili per il componente.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: Esportare report](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Procedura: Eseguire l'analisi guidata di preparazione aggiornamento](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Risoluzione dei problemi di aggiornamento](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Procedure per Preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
