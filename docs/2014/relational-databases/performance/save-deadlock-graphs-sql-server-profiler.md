---
title: Salvare eventi Deadlock Graph (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], saving deadlock graphs
- graphs [SQL Server]
- saving deadlock graphs
ms.assetid: bf1fc906-abd6-4a89-842e-da0d66b2defe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 33757ad1f8085ce141b8e206f2c3fd99c7dcba90
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818276"
---
# <a name="save-deadlock-graphs-sql-server-profiler"></a>Salvare eventi Deadlock Graph (SQL Server Profiler)
  In questo argomento viene descritto come salvare un evento Deadlock Graph utilizzando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Gli eventi Deadlock Graph vengono salvati come file XML.  
  
### <a name="to-save-deadlock-graph-events-separately"></a>Per salvare gli eventi Deadlock Graph separatamente  
  
1.  Scegliere **Nuova traccia** dal menu **File**e quindi connettersi a un'istanza di SQL Server.  
  
     Verrà visualizzata la finestra di dialogo **Proprietà traccia**.  
  
    > [!NOTE]  
    >  Se l'opzione **Avvia traccia non appena viene stabilita una connessione** è selezionata, la finestra di dialogo **Proprietà traccia**non viene visualizzata e viene invece avviata la traccia. Per disabilitare questa impostazione, scegliere **Opzioni**dal menu **Strumenti**e deselezionare la casella di controllo **Avvia traccia non appena viene stabilita una connessione** .  
  
2.  Nella finestra di dialogo Proprietà traccia digitare un nome per la traccia nella casella**Nome traccia** .  
  
3.  Nell'elenco **Modello** selezionare un modello di traccia sul quale basare la traccia oppure selezionare **Vuoto** per non utilizzare alcun modello.  
  
4.  Eseguire una delle operazioni seguenti:  
  
    -   Selezionare la casella di controllo**Salva nel file** per acquisire la traccia in un file. Specificare un valore per l'opzione **Dimensioni massime del file**.  
  
         Facoltativamente selezionare le caselle di controllo **Consenti rollover dei file** e **Dati di traccia elaborati dal server**.  
  
    -   Selezionare la casella di controllo **Salva nella tabella** per acquisire la traccia in una tabella di database.  
  
         Facoltativamente selezionare la casella di controllo **Numero massimo di righe**e specificare un valore.  
  
5.  Facoltativamente, selezionare la casella di controllo **Data e ora di arresto della traccia** e specificare una data e un'ora di arresto della traccia.  
  
6.  Fare clic sulla scheda **Selezione eventi**.  
  
7.  Nella colonna di dati **Eventi**espandere la categoria di eventi **Locks**e quindi selezionare la casella di controllo **Deadlock graph**. Se la categoria di eventi Locks non è disponibile, selezionare **Mostra tutti gli eventi** per visualizzarla.  
  
     Verrà visualizzata la finestra di dialogo **Impostazioni estrazione event**viene aggiunta alla finestra di dialogo **Proprietà traccia**.  
  
8.  Nella scheda **Impostazioni estrazione eventi**fare clic su **Salva eventi deadlock XML separatamente**.  
  
9. Nella finestra di dialogo **Salva con nome** digitare il nome del file nel quale memorizzare gli eventi Deadlock Graph.  
  
10. Fare clic su **Tutti i batch deadlock XML in un singolo file** per salvare tutti gli eventi Deadlock Graph in un file XML singolo oppure fare clic su **Crea un file distinto per ogni singolo batch deadlock XML**per creare un nuovo file XML per ogni evento Deadlock Graph.  
  
 Dopo aver salvato il file deadlock, è possibile aprire il file in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Apertura, visualizzazione e stampa di un file deadlock &#40;SQL Server Management Studio&#41;](open-view-and-print-a-deadlock-file-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Analizzare deadlock con SQL Server Profiler](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)  
  
  
