---
title: Strumenti e approcci per l'elaborazione (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- process [Analysis Services]
- processing [Analysis Services]
ms.assetid: 82347a16-4145-4655-8adf-2a300f1fdf99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a6bcc8e830c682c800f7dbdd586b25b88ca8577f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "69530937"
---
# <a name="tools-and-approaches-for-processing-analysis-services"></a>Strumenti e approcci per l'elaborazione (Analysis Services)
  L'elaborazione è un'operazione durante la quale tramite Analysis Services viene effettuata una query su un'origine dati relazionale e gli oggetti di Analysis Services vengono popolati utilizzando i dati ottenuti.  
  
 Un amministratore di sistema di Analysis Services può eseguire e monitorare l'elaborazione degli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzando i seguenti approcci:  
  
-   Eseguire l'analisi di impatto per comprendere le dipendenze tra oggetti e l'ambito delle operazioni  
  
-   Elaborare oggetti singoli in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Elaborare oggetti singoli o più oggetti in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   Eseguire l'analisi di impatto per esaminare un elenco di oggetti correlati che resteranno non elaborati in conseguenza dell'azione corrente  
  
-   Generare ed eseguire uno script in una finestra Query XMLA di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per elaborare oggetti singoli o più oggetti  
  
-   Utilizzare cmdlet di PowerShell per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   Utilizzare flussi di controllo e attività nei pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
-   Monitorare l'elaborazione con SQL Server Profiler  
  
-   Programmare una soluzione personalizzata utilizzando AMO. Per altre informazioni, vedere [Programmazione di oggetti OLAP in AMO](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-basic-objects).  
  
 L'elaborazione è un'operazione estremamente configurabile, controllata da un set di opzioni che determinano se si verifica un'elaborazione completa o incrementale a livello di oggetto. Per altre informazioni sulle opzioni di elaborazione e gli oggetti, vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md) ed [Elaborazione di oggetti di Analysis Services](processing-analysis-services-objects.md).  
  
> [!NOTE]  
>  In questo argomento vengono descritti gli strumenti e gli approcci per l'elaborazione di modelli multidimensionali. Per ulteriori informazioni sull'elaborazione di modelli tabulari, vedere elaborare i dati del [database, della tabella o della partizione](../tabular-models/process-database-table-or-partition-analysis-services.md) ed [elaborare i dati &#40;SSAS tabulare&#41;](../process-data-ssas-tabular.md).  
  
### <a name="processing-objects-in-sql-server-management-studio"></a>Gestione di oggetti in SQL Server Management Studio  
  
1.  Avviare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e connettersi ad Analysis Services.  
  
2.  Fare clic con il pulsante destro del mouse sull'oggetto di Analysis Services che si vuole elaborare, quindi scegliere **Elabora**. È possibile elaborare dati a uno qualsiasi dei livelli seguenti:  
  
    -   Database  
  
    -   Cubi  
  
    -   Gruppi di misure o singole partizioni nel gruppo di misure  
  
    -   Dimensioni  
  
    -   Modelli di data mining  
  
    -   Strutture di data mining  
  
     Gli oggetti di Analysis Services sono gerarchici. Se si sceglie database, l'elaborazione può essere effettuata per tutti gli oggetti contenuti nel database. L'effettiva esecuzione dell'elaborazione dipende dall'opzione di elaborazione selezionata e dallo stato dell'oggetto. In particolare, se un oggetto non è elaborato, l'elaborazione del relativo oggetto padre comporterà l'elaborazione di tale oggetto. Per altre informazioni sulle dipendenze tra oggetti, vedere [Elaborazione di oggetti di Analysis Services](processing-analysis-services-objects.md).  
  
3.  Nella finestra di dialogo **Elabora** , in **Opzioni elaborazione**usare il valore predefinito fornito o selezionare un'opzione diversa dall'elenco. Per altre informazioni su ogni opzione, vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
4.  Fare clic su **Analisi di impatto** per identificare ed eventualmente elaborare gli oggetti dipendenti sui quali influisce l'elaborazione degli oggetti elencati nella finestra di dialogo Elabora.  
  
5.  Facoltativamente, fare clic su **Modifica impostazioni** per modificare l'ordine di elaborazione, il comportamento di elaborazione in relazione a tipi specifici di errori e altre impostazioni.  
  
6.  Fare clic su **OK**.  
  
     Nella finestra di dialogo Stato elaborazione viene visualizzato stato corrente per ogni comando. Se un messaggio di stato è troncato, è possibile fare clic su **Visualizza dettagli** per leggere l'intero messaggio.  
  
### <a name="processing-objects-in-sql-server-data-tools"></a>Elaborazione di oggetti in SQL Server Data Tools  
  
1.  Avviare [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e aprire un progetto distribuito.  
  
2.  In Esplora soluzioni espandere la cartella **Dimensioni** del progetto distribuito.  
  
3.  Fare clic con il pulsante destro del mouse su una dimensione, quindi scegliere **Elabora**. È possibile fare clic con il pulsante destro del mouse su più dimensioni per elaborare più oggetti contemporaneamente. Per altre informazioni, vedere [Elaborazione batch &#40;Analysis Services&#41;](batch-processing-analysis-services.md).  
  
4.  Nella finestra di dialogo **** di elaborazione, in **Elenco oggetti** verificare che l’opzione per la colonna **Opzioni elaborazione**sia **Elaborazione completa**. In caso contrario, in **Opzioni elaborazione**fare clic sull’opzione e selezionare **Elaborazione completa** nell'elenco a discesa.  
  
5.  Fare clic su **Esegui**.  
  
6.  Al termine dell'elaborazione, fare clic su **Chiudi**.  
  
##  <a name="run-impact-analysis-to-identify-object-dependencies-and-scope-of-operations"></a><a name="bkmk_impactanalysis"></a>Eseguire l'analisi di effetto per identificare le dipendenze tra oggetti e l'ambito delle operazioni  
  
1.  Prima di elaborare un oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], è possibile analizzare l'effetto sugli oggetti correlati facendo clic su **Analisi di impatto** in una delle finestre di dialogo **Elabora oggetti** .  
  
2.  Fare clic con il pulsante destro del mouse su una dimensione, un cubo, un gruppo di misure o una partizione per aprire una finestra di dialogo **Elabora oggetti** .  
  
3.  Fare clic su **Analisi di impatto**. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue l’analisi del modello e indica i requisiti di rielaborazione per gli oggetti correlati a quello che è stato selezionato per l’elaborazione.  
  
### <a name="processing-objects-using-xmla"></a>Elaborazione di oggetti tramite XMLA  
  
1.  Avviare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e connettersi ad Analysis Services.  
  
2.  Fare clic con il pulsante destro del mouse sull'oggetto da elaborare, quindi scegliere **Elabora**.  
  
3.  Nella finestra di dialogo **Elabora** selezionare l'opzione di elaborazione che si vuole utilizzare. Modificare eventuali altre impostazioni. Eseguire l'analisi di impatto per identificare le eventuali modifiche che potrebbe essere necessario apportare.  
  
4.  Fare clic su **Script** nella schermata **Elabora oggetti** .  
  
     Verrà generato uno script XMLA e verrà aperta una finestra Query XMLA di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
5.  Chiudere la finestra di dialogo. Lo script contiene il comando e le opzioni di elaborazione specificati nella finestra di dialogo.  
  
6.  Facoltativamente, è possibile continuare ad aggiungere allo script se si desidera elaborare oggetti aggiuntivi nello stesso batch. Per continuare, ripetere i passaggi precedenti, accodando lo script generato in modo da disporre di un solo script per tutte le operazioni di elaborazione. Per un esempio, vedere [Pianificare attività amministrative SSAS con SQL Server Agent](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md).  
  
7.  Sulla barra dei menu scegliere **Esegui**dal menu **Query**.  
  
### <a name="processing-objects-using-powershell"></a>Elaborazione di oggetti tramite PowerShell  
  
1.  Avviando questa versione di SQL Server, è possibile utilizzare i cmdlet di PowerShell per Analysis Services per l'elaborazione di oggetti. È possibile eseguire i cmdlet seguenti in modo interattivo o in script:  
  
    -   [Cmdlet Invoke-ProcessCube](/powershell/module/sqlserver/invoke-processcube)  
  
    -   [Cmdlet Invoke-ProcessDimension](/powershell/module/sqlserver/invoke-processdimension)  
  
    -   [Cmdlet Invoke-ProcessPartition](/powershell/module/sqlserver/invoke-processpartition)  
  
    -   [cmdlet Invoke-ASCmd](/powershell/module/sqlserver/invoke-ascmd)che può essere usato per eseguire script XMLA, MDX o DMX che includono comandi di elaborazione.  
  
### <a name="monitoring-object-processing-using-sql-server-profiler"></a>Monitoraggio dell'elaborazione degli oggetti utilizzando SQL Server Profiler  
  
1.  Connettersi a un'istanza di Analysis Services in SQL Server Profiler.  
  
2.  In Selezione eventi fare clic su **Mostra tutti gli eventi** per aggiungere tutti gli eventi all'elenco.  
  
3.  Scegliere gli eventi seguenti:  
  
    -   **Inizio del comando** e **Fine del comando** per mostrare l'inizio e la fine dell'elaborazione  
  
    -   **Errore** per acquisire eventuali errori  
  
    -   **Inizio del report di stato**, **Stato corrente del report di stato**e **Fine del report di stato** per creare un report sullo stato dell'elaborazione e mostrare le query SQL utilizzate per recuperare i dati  
  
    -   **Inizio dell'esecuzione di script MDX** e **Fine dell'esecuzione di script MDX** per mostrare i calcoli del cubo  
  
    -   Facoltativamente, aggiungere eventi di blocco in caso di diagnosi di problemi di prestazioni correlati all'elaborazione  
  
### <a name="process-analysis-services-objects-using-integration-services"></a>Elaborare oggetti di Analysis Services utilizzando Integration Services  
  
1.  In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]creare un pacchetto in cui viene usata l'attività Elaborazione Analysis Services per popolare automaticamente gli oggetti con nuovi dati quando si eseguono aggiornamenti regolari nel database relazionale di origine.  
  
2.  In **Casella degli strumenti SSIS**fare doppio clic su **Attività Elaborazione Analysis Services** per aggiungerla al pacchetto.  
  
3.  Modificare l'attività per specificare una connessione al database, gli oggetti da elaborare e l'opzione di elaborazione. Per ulteriori informazioni sull'implementazione di questa attività, vedere [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborazione di oggetti del modello multidimensionale](processing-a-multidimensional-model-analysis-services.md)  
  
  
