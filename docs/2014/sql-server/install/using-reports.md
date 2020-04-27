---
title: Uso dei report | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- overriding reports
- Upgrade Advisor Report Viewer
- reports [Upgrade Advisor], about reports
- formatting reports
- resolved issues [Upgrade Advisor]
- distributing reports [Reporting Services]
- filtering reports [Reporting Services]
- removing report items
- viewing reports
- rerunning analysis
- information issues [Upgrade Advisor]
- deleting report items
- icons [Upgrade Advisor]
- Upgrade Advisor [SQL Server], reports
- sending reports
- blocking issues [Upgrade Advisor]
- sharing reports
- reports [Upgrade Advisor]
- SQL Server Upgrade Advisor, reports
- modifying reports
- distributing reports [Reporting Services], about report distribution
- warnings [Upgrade Advisor]
- analyzing system [Upgrade Advisor], reports
ms.assetid: 4a3cb94a-a7ac-4cec-94c7-db26fcf6d161
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc3a08e707f6b51059145c69fdee15f78c933135
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091227"
---
# <a name="using-reports"></a>Utilizzo dei report
  Per ogni componente e, se necessario, per ogni istanza analizzata tramite l'Analisi guidata di Preparazione aggiornamento su un server viene generato un report distinto, in cui sono forniti dettagli su problemi noti che influiscono su un aggiornamento. Il report contiene inoltre collegamenti a informazioni e ad azioni consigliate per la risoluzione dei problemi identificati.  
  
> [!NOTE]  
>  Se il Visualizzatore report di preparazione aggiornamento non trova alcun report nella directory dei report predefinita, è possibile caricare un report da una directory diversa utilizzando il collegamento **Apri report** .  
  
## <a name="viewing-reports"></a>Visualizzazione dei report  
 Utilizzare il Visualizzatore report di Preparazione aggiornamento per visualizzare i report di Preparazione aggiornamento. Per visualizzare i report, nella pagina iniziale di preparazione aggiornamento fare clic su **Avvia Visualizzatore report di preparazione aggiornamento**.  
  
 Dopo avere caricato un report per un server, è possibile selezionare un componente per cui visualizzare i problemi di aggiornamento. È possibile applicare un filtro dalla casella **Filtra** per per vedere quanto segue:  
  
-   Tutti i problemi  
  
-   Tutti i problemi di aggiornamento  
  
-   Problemi di pre-aggiornamento  
  
-   Tutti i problemi di migrazione  
  
-   Problemi risolti  
  
-   Problemi irrisolti  
  
 Se il report contiene più di 20 problemi, è possibile passare al gruppo di problemi successivo o precedente facendo clic su **Avanti 20** o **20 precedente** nella parte superiore o inferiore dell'elenco problemi.  
  
 È possibile visualizzare fino a cinque report salvati selezionando i report dall'elenco a discesa **report** . I report vengono elencati in base al valore timestamp che indica la data e l'ora in cui sono stati generati.  
  
## <a name="report-format"></a>Formato dei report  
 Il visualizzatore di report suddivide i problemi in tre colonne. Ogni problema è comprimibile, in modo che sia possibile nascondere la descrizione e visualizzare solo le informazioni essenziali.  
  
 La prima colonna è la colonna **priorità** . Le icone indicano l'importanza di ogni problema: viene visualizzato un cerchio rosso con una X per problemi importanti o che bloccano l'aggiornamento oppure un triangolo giallo con un punto esclamativo per problemi paragonabili a messaggi di avviso o informativi. La seconda colonna, **quando correggere**, indica quando è necessario risolvere il problema. È possibile ordinare il report in modo che sia la colonna **importanza** o **quando correggere** . Nella terza colonna, **Descrizione**, viene elencato il titolo del problema.  
  
 È possibile espandere un problema per visualizzare informazioni aggiuntive, un collegamento a informazioni dettagliate sulla risoluzione e un collegamento per visualizzare i dettagli del problema. Quando si fa clic sul collegamento per ottenere informazioni dettagliate per il problema, verrà visualizzato un argomento della Guida con informazioni e istruzioni per risolverlo. Dopo aver risolto un problema o aver gestito gli elementi dell'azione, è possibile contrassegnare i problemi come completi selezionando la casella di controllo **questo problema è stato risolto** . Se si desidera rimuovere i problemi risolti dall'elenco dei problemi di aggiornamento, fare clic su **Aggiorna**. Il problema non viene visualizzato di nuovo fino a quando non si esegue l'analisi guidata di preparazione aggiornamento sullo stesso componente o si applica il filtro **problemi risolti** dall'opzione **Filtra per** .  
  
## <a name="report-files"></a>File di report  
 L'analisi guidata di preparazione aggiornamento consente di creare report nella\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directory My Documents upgrade Advisor\110\Reports e di creare una sottodirectory per ogni server analizzato. I file di report sono in formato XML e seguono una convenzione di denominazione specifica. Quando si avvia il Visualizzatore report di Preparazione aggiornamento, vengono visualizzati i file di report della directory predefinita. Se vengono copiati file di report in questa cartella, è necessario che rispettino la convenzione di denominazione, altrimenti non verranno visualizzati automaticamente.  
  
 Se si desidera condividere le informazioni con altri utenti, è possibile inviare il report XML. In alternativa, se si desidera utilizzare un'altra applicazione, è possibile esportare il report in un file con valori delimitati da virgole da utilizzare per creare un foglio di calcolo, un file di testo o un messaggio di posta elettronica.  
  
## <a name="see-also"></a>Vedi anche  
 [Procedura: visualizzazione di un report di preparazione aggiornamento](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)   
 [Procedura: esportazione di report](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Procedura: filtrare i report](../../../2014/sql-server/install/how-to-filter-reports.md)   
 [Risoluzione dei problemi di aggiornamento](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
