---
title: Ottimizzazione di un carico di lavoro | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- workloads [SQL Server], tuning
ms.assetid: 6229bf3f-1182-4bc6-8451-cedc37f4b62e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3dd87c1e2bd08ce5bb1d05e9d51d92e3f62bcc7a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66110191"
---
# <a name="tuning-a-workload"></a>Ottimizzazione di un carico di lavoro
  Per individuare la migliore struttura fisica di database per l'esecuzione di query sulle tabelle e i database selezionati per l'ottimizzazione, è possibile utilizzare Ottimizzazione guidata motore di database.  
  
 In questa attività viene utilizzato il database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Per una maggiore sicurezza, i database di esempio non vengono installati per impostazione predefinita. Per installare i database di esempio, vedere la pagina [Installazione degli esempi e dei database di esempio di SQL Server](http://sqlserversamples.codeplex.com).  
  
### <a name="tune-a-workload-transact-sql-script-file"></a>Per ottimizzare un file script Transact-SQL del carico di lavoro  
  
1.  Copiare una o più istruzioni SELECT di esempio da "A. Utilizzo dell'istruzione SELECT per il recupero di righe e colonne" in [Esempi di istruzioni SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-examples-transact-sql) e incollare le istruzioni nell'Editor di query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Salvare il file con il nome **MyScript.sql** in una directory in cui sia possibile individuarlo facilmente.  
  
2.  Avviare Ottimizzazione guidata motore di database. Vedere [Avvio dello strumento Ottimizzazione guidata motore di database](../../relational-databases/performance/database-engine-tuning-advisor.md).  
  
3.  Nel riquadro destro della GUI di Ottimizzazione guidata motore di database digitare **MySession** in **Nome sessione**.  
  
4.  Selezionare **File** per **Carico di lavoro**e fare clic sul pulsante **Consente di cercare un file di carico di lavoro** per trovare il file **MyScript.sql** salvato nel passaggio 1.  
  
5.  Selezionare [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] nell'elenco **Database per l'analisi del carico di lavoro** , selezionare [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] nella griglia **Selezionare i database e le tabelle da ottimizzare** e lasciare selezionata l'opzione **Salva log di ottimizzazione** . **Database per l'analisi del carico di lavoro** specifica il primo database a cui ottimizzazione guidata motore di database si connette durante l'ottimizzazione di un carico di lavoro. Dopo l'inizio dell'ottimizzazione, Ottimizzazione guidata motore di database si connette ai database specificati dalle istruzioni `USE DATABASE` contenute nel carico di lavoro.  
  
6.  Fare clic sulla scheda **Opzioni di ottimizzazione** . Non verranno impostate opzioni di ottimizzazione per questa procedura, ma occorrerà un po' di tempo per rivedere le opzioni di ottimizzazione predefinite. Premere F1 per visualizzare la Guida relativa a questa pagina a schede. Fare clic su **Opzioni avanzate** per visualizzare le opzioni di ottimizzazione aggiuntive. Fare clic su **?** nella finestra di dialogo **Opzioni di ottimizzazione avanzate** per ottenere informazioni sulle opzioni di ottimizzazione visualizzate. Fare clic su **Annulla** per chiudere la finestra di dialogo **Opzioni di ottimizzazione avanzate** lasciando selezionate le opzioni predefinite.  
  
7.  Fare clic sul pulsante **Avvia analisi** sulla barra degli strumenti. Mentre Ottimizzazione guidata motore di database analizza il carico di lavoro, è possibile monitorare lo stato nella scheda **stato** . Al termine dell'ottimizzazione, verrà visualizzata la scheda **indicazioni** .  
  
     Se viene visualizzato un errore relativo alla data e all'ora di arresto dell'ottimizzazione, controllare l'ora di **arresto** nella scheda principale **Opzioni di ottimizzazione** . Assicurarsi che la data e l'ora di **arresto** siano maggiori della data e dell'ora correnti e, se necessario, modificarle.  
  
8.  Dopo aver completato l'analisi, salvare le indicazioni come script [!INCLUDE[tsql](../../includes/tsql-md.md)] scegliendo **Salva indicazioni** dal menu **Azioni** . Nella finestra di dialogo **Salva con nome** trovare la directory in cui si vuole salvare lo script delle indicazioni e digitare il nome file **MyRecommendations**.  
  
## <a name="summary"></a>Summary  
 In questo modo è stata completata l'ottimizzazione di un carico di lavoro di un'istruzione SELECT semplice sul database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Ottimizzazione guidata motore di database accetta inoltre file di traccia e tabelle [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] come carichi di lavoro da ottimizzare. Nell'attività successiva verranno illustrate le procedure per visualizzare e interpretare le indicazioni scaturite dall'esercitazione sull'ottimizzazione.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Visualizzazione delle indicazioni di ottimizzazione](lesson-1-2-viewing-tuning-recommendations.md)  
  
  
