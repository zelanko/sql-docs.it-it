---
title: Salvare gli eventi Showplan XML Statistics Profile in file distinti (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: df393f13-d538-4d94-8155-9c2fdf5f755d
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 330ce947c7d70aaef5c3409484102284db03802c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53349479"
---
# <a name="save-showplan-xml-statistics-profile-events-separately-sql-server-profiler"></a>Salvare gli eventi Showplan XML Statistics Profile in file distinti (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questo argomento descrive la procedura da seguire per salvare gli eventi **Showplan XML Statistics Profile** acquisiti in tracce in file SQLPlan distinti tramite [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. È possibile aprire i file di eventi **Showplan XML Statistics Profile** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per visualizzare graficamente il piano di esecuzione di ogni evento.  
  
## <a name="save-showplan-xml-statistics-profile-events-separately"></a>Salvare eventi Showplan XML Statistics Profile in file distinti  
  
1. Scegliere **Nuova traccia** dal menu **File** e quindi connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
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
  
7. Nella colonna di dati **Eventi** espandere la categoria di eventi **Prestazioni** e quindi selezionare la casella di controllo **Showplan XML Statistics Profile**. Se la categoria di eventi **Prestazioni** non è visualizzata, selezionare la casella di controllo **Mostra tutti gli eventi**.  
  
     La scheda **Impostazioni estrazione eventi** viene aggiunta alla finestra di dialogo **Proprietà traccia**.  
  
8. Nella scheda **Impostazioni estrazione eventi** selezionare la casella di controllo **Salva eventi Showplan XML separatamente**.  
  
9. Nella finestra di dialogo **Salva con nome** immettere un nome per il file in cui archiviare gli eventi **Showplan XML Statistics Profile** .  
  
10. Selezionare **All batches in a single file** (Tutti i batch in un singolo file) per salvare tutti gli eventi **Showplan XML Statistics Profile** in un singolo file XML. In alternativa, selezionare **Crea un file distinto per ogni singolo batch Showplan XML** per creare un nuovo file XML per ogni evento **Showplan XML Statistics Profile**.  
  
11. Per visualizzare il file di eventi **Showplan XML Statistics Profile** in SQL Server Management Studio, scegliere **Apri** dal menu **File** e quindi fare clic su **File**. Andare alla directory in cui è stato salvato il file o i file di eventi **Showplan XML Statistics Profile** per selezionare il file desiderato e quindi aprirlo. I file di eventi**Showplan XML Statistics Profile** sono contraddistinti dall'estensione SQLPlan.  
  
## <a name="see-also"></a>Vedere anche  
 [Analizzare query con risultati Showplan in SQL Server Profiler](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  
