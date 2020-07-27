---
title: Salvare eventi Deadlock Graph (SQL Server Profiler) | Microsoft Docs
description: Informazioni su come salvare un evento Deadlock Graph usando SQL Server Profiler. Gli eventi Deadlock Graph vengono salvati come file XML.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], saving deadlock graphs
- graphs [SQL Server]
- saving deadlock graphs
ms.assetid: bf1fc906-abd6-4a89-842e-da0d66b2defe
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 874597d5d62f13556072fb129931fa9e4faf1a85
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458729"
---
# <a name="save-deadlock-graphs-sql-server-profiler"></a>Salvare eventi Deadlock Graph (SQL Server Profiler)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  In questo argomento viene descritto come salvare un evento Deadlock Graph utilizzando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Gli eventi Deadlock Graph vengono salvati come file XML.  
  
## <a name="save-deadlock-graph-events-separately"></a>Salvare gli eventi Deadlock Graph separatamente  
  
1. Scegliere **Nuova traccia** dal menu **File** e quindi connettersi a un'istanza di SQL Server.  
  
     Verrà visualizzata la finestra di dialogo **Proprietà traccia** .  
  
    > [!NOTE]  
    >  Se la casella di controllo **Avvia traccia non appena viene stabilita una connessione** è selezionata, la finestra di dialogo **Proprietà traccia** non viene visualizzata e viene invece avviata la traccia. Per disattivare questa impostazione, scegliere **Opzioni** dal menu **Strumenti** e deselezionare la casella di controllo **Avvia traccia non appena viene stabilita una connessione**.  
  
2. Nella finestra di dialogo **Proprietà traccia** digitare un nome per la traccia nella casella **Nome traccia** .  
  
3. Nell'elenco **Modello** selezionare un modello di traccia su cui basare la traccia. Se non si vuole usare alcun modello, selezionare **Vuoto**.  
  
4. Eseguire una delle operazioni seguenti:  
  
    -   Per acquisire la traccia in un file selezionare la casella di controllo **Salva nel file**. Specificare un valore per l'opzione **Dimensioni massime del file**.  
  
         Se lo si desidera, selezionare le caselle di controllo **Consenti rollover dei file** e **Dati di traccia elaborati dal server** . 
  
    -   Per acquisire la traccia in una tabella di database, selezionare la casella di controllo **Salva nella tabella**.  
  
         Facoltativamente selezionare **Numero massimo di righe** e specificare un valore.  
  
5. Facoltativamente, selezionare la casella di controllo **Data e ora di arresto della traccia** e specificare una data e un'ora di arresto della traccia. 
  
6. Fare clic sulla scheda **Selezione eventi**.  
  
7. Nella colonna di dati **Eventi** espandere la categoria di eventi **Locks** e quindi selezionare la casella di controllo **Deadlock Graph**. Se la categoria di eventi **Locks** non è disponibile, selezionare la casella di controllo **Mostra tutti gli eventi** per visualizzarla.  
  
     La scheda **Impostazioni estrazione eventi** viene aggiunta alla finestra di dialogo **Proprietà traccia**.  
  
8. Nella scheda **Impostazioni estrazione eventi** fare clic su **Salva eventi deadlock XML separatamente**.  
  
9. Nella finestra di dialogo **Salva con nome** digitare il nome del file nel quale memorizzare gli eventi Deadlock Graph.  
  
10. Selezionare **Tutti i batch deadlock XML in un singolo file** per salvare tutti gli eventi Deadlock Graph in un singolo file XML. In alternativa selezionare **Crea un file distinto per ogni singolo batch deadlock XML** per creare un nuovo file XML per ogni evento Deadlock Graph.  
  
 Dopo aver salvato il file deadlock, è possibile aprire il file in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Aprire, visualizzare e stampare un file deadlock &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/open-view-and-print-a-deadlock-file-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Analizzare deadlock con SQL Server Profiler](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)  
  
  
