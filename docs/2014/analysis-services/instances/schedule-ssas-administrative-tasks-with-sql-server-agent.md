---
title: Pianificare attività amministrative SSAS con SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2d1484b3-51d9-48a0-93d2-0c3e4ed22b87
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b24e99ac31b126888a1fa49f3ef5547a4f82dda
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079679"
---
# <a name="schedule-ssas-administrative-tasks-with-sql-server-agent"></a>Pianificare attività amministrative SSAS con SQL Server Agent
  Usando il servizio SQL Server Agent, è possibile pianificare l'esecuzione delle attività amministrative di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nell'ordine e agli orari necessari. Le attività pianificate consentono di automatizzare processi eseguiti in cicli regolari o prevedibili. È possibile pianificare l'esecuzione di attività amministrative, ad esempio l'elaborazione di cubi, nei periodi in cui l'attività aziendale è ridotta. È inoltre possibile determinare l'ordine di esecuzione delle attività creando passaggi di processo in un processo di SQL Server Agent. È possibile ad esempio elaborare un cubo ed eseguirne quindi un backup.  
  
 I passaggi di processo consentono di controllare il flusso dell'esecuzione. Se uno dei processi ha esito negativo, è possibile configurare SQL Server Agent per continuare a eseguire le attività rimanenti o per arrestare l'esecuzione. È inoltre possibile configurare SQL Server Agent per l'invio di notifiche relative all'esito positivo o negativo dell'esecuzione di un processo.  
  
 In questo argomento è disponibile una procedura dettagliata che illustra due modalità di utilizzo di SQL Server Agent per eseguire script XMLA. Nel primo esempio viene dimostrato come pianificare l'elaborazione di una singola dimensione. Nel secondo esempio viene illustrato come combinare attività di elaborazione in uno singolo script eseguito in una pianificazione. Per completare la procedura dettagliata, è necessario soddisfare i requisiti riportati di seguito.  
  
## <a name="prerequisites"></a>Prerequisiti  
 È necessario che il servizio SQL Server Agent sia installato.  
  
 Per impostazione predefinita, i processi vengono eseguiti con l'account del servizio. Nelle [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], l'account predefinito per SQL Server Agent è NT Service\SQLAgent$\<NomeIstanza >. Per eseguire un backup o un'attività di elaborazione, è necessario utilizzare un account amministratore di sistema nell'istanza di Analysis Services. Per altre informazioni, vedere [Concedi autorizzazioni di amministratore del Server &#40;Analysis Services&#41;](grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
 È consigliabile utilizzare un database di test. È possibile distribuire il database di esempio multidimensionale AdventureWorks o un progetto dell'esercitazione multidimensionale di Analysis Services da utilizzare in questa procedura dettagliata. Per altre informazioni, vedere [Installare dati di esempio e progetti per l'esercitazione di modellazione multidimensionale di Analysis Services](../install-sample-data-and-projects.md).  
  
## <a name="example-1-processing-a-dimension-in-a-scheduled-task"></a>Esempio 1: Elaborazione di una dimensione in un'attività pianificata  
 In questo esempio viene illustrato come creare e pianificare un processo che elabora una dimensione.  
  
 Un'attività pianificata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è uno script XMLA incorporato in un processo di SQL Server Agent. L'esecuzione di questo processo è pianificata per l'esecuzione negli orari e con la frequenza desiderati. Poiché SQL Server Agent è un componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], per la creazione e la pianificazione di un'attività amministrativa verranno utilizzati sia il Motore di database che [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
###  <a name="bkmk_CreateScript"></a> Creare uno script per l'elaborazione di una dimensione in un processo di SQL Server Agent  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Aprire una cartella di database e individuare una dimensione. Fare clic con il pulsante destro del mouse sulla dimensione e scegliere **Elabora**.  
  
2.  Nella finestra di dialogo **Elaborazione dimensione** , nella colonna **Opzioni elaborazione** di **Elenco oggetti**, verificare che l'opzione per la colonna sia **Elaborazione completa**. In caso contrario, in **Opzioni elaborazione**fare clic sull'opzione e quindi selezionare **Elaborazione completa** nell'elenco a discesa.  
  
3.  Fare clic su **Script**.  
  
     Questo passaggio apre una finestra **Query XML** contenente lo script XMLA che elabora la dimensione.  
  
4.  Nella finestra di dialogo **Elaborazione dimensione** fare clic su **Annulla** per chiudere la finestra di dialogo.  
  
5.  Nella finestra **Query XMLA** selezionare lo script XMLA, fare clic con il pulsante destro del mouse su tale script e scegliere **Copia**.  
  
     In questo passaggio lo script XMLA viene copiato negli Appunti di Windows. È possibile lasciare lo script XMLA negli Appunti o incollarlo nel Blocco note o un altro editor di testo. Di seguito è riportato un esempio di script XMLA.  
  
    ```  
    <Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Account</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
###  <a name="bkmk_ProcessJob"></a> Creare e pianificare il processo di elaborazione della dimensione  
  
1.  Connettersi a un'istanza del motore di database e quindi aprire Esplora oggetti.  
  
2.  Espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse su **Processi** e selezionare **Nuovo processo**.  
  
4.  Nella finestra di dialogo **Nuovo processo** immettere il nome del processo nella casella **Nome**.  
  
5.  In **Selezione pagina**selezionare **Passaggi**e quindi fare clic su **Nuovo**.  
  
6.  Nella finestra di dialogo **Nuovo passaggio di processo** immettere il nome del passaggio nella casella **Nome passaggio**.  
  
7.  In **Server** digitare **localhost** per un'istanza predefinita di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e **localhost\\**\<*nome istanza*> per un'istanza denominata.  
  
     Se si eseguirà il processo da un computer remoto, utilizzare il nome del server e il nome dell'istanza in cui il processo verrà eseguito. Usare il formato \< *nome server*> per un'istanza predefinita, e \< *nome del server*>\\<*istanza nome*> per un'istanza denominata.  
  
8.  In **Tipo**selezionare **Comando di SQL Server Analysis Services**.  
  
9. In **Comando**fare clic con il pulsante destro del mouse e scegliere **Incolla**. Lo script XMLA generato nel passaggio precedente verrà visualizzato nella finestra di comando.  
  
10. Fare clic su **OK**.  
  
11. In **Selezione pagina**fare clic su **Pianificazioni**e quindi su **Nuovo**.  
  
12. Nella finestra di dialogo **Nuova pianificazione processo** immettere il nome della pianificazione nella casella **Nome**e fare clic su **OK**.  
  
     In questo passaggio viene creata una pianificazione per domenica alle 12.00 AM. Nel passaggio successivo verrà illustrato come eseguire manualmente il processo. È inoltre possibile specificare una pianificazione che esegue il processo mentre viene monitorato.  
  
13. Nella finestra di dialogo **Nuovo processo** fare clic su **OK**.  
  
14. In **Esplora oggetti**espandere **Processi**, fare clic con il pulsante destro del mouse sul processo creato e quindi selezionare **Inizia processo al passaggio**.  
  
     Poiché il processo include un solo passaggio, verrà eseguito immediatamente. Se il processo è costituito da più di un passaggio, è possibile selezionare quello da cui dovrà iniziare il processo.  
  
15. Al termine del processo fare clic su **Chiudi**.  
  
## <a name="example-2-batch-processing-a-dimension-and-a-partition-in-a-scheduled-task"></a>Esempio 2: Una dimensione e una partizione in un'attività pianificata per l'elaborazione batch  
 Le procedure in questo esempio dimostrano come creare e pianificare un processo per l'elaborazione batch di una dimensione database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e contemporaneamente per l'elaborazione di una partizione del cubo che dipende dalla dimensione per l'aggregazione. Per altre informazioni sull'elaborazione batch di oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Elaborazione batch &#40;Analysis Services&#41;](../multidimensional-models/batch-processing-analysis-services.md).  
  
###  <a name="bkmk_BatchProcess"></a> Creare uno script per l'elaborazione batch di una dimensione e una partizione in un processo di SQL Server Agent  
  
1.  Usando lo stesso database, espandere **Dimensioni**, fare clic con il pulsante destro del mouse sulla dimensione **Customer** e scegliere **Elabora**.  
  
2.  Nella finestra di dialogo **Elaborazione dimensione** , nella colonna **Opzioni elaborazione** di **Elenco oggetti**, verificare che l'opzione per la colonna sia **Elaborazione completa**.  
  
3.  Fare clic su **Script**.  
  
     Questo passaggio apre una finestra **Query XML** contenente lo script XMLA che elabora la dimensione.  
  
4.  Nella finestra di dialogo **Elaborazione dimensione** fare clic su **Annulla** per chiudere la finestra di dialogo.  
  
5.  Espandere **Cubi**, **Adventure Works**, **Gruppi di misure**, **Internet Sales**e **Partizioni**, fare clic con il pulsante destro del mouse sull'ultima partizione nell'elenco e quindi scegliere **Elabora**.  
  
6.  Nella finestra di dialogo **Elaborazione partizione** , nella colonna **Opzioni elaborazione** di **Elenco oggetti**, verificare che l'opzione per la colonna sia **Elaborazione completa**.  
  
7.  Fare clic su **Script**.  
  
     Questo passaggio apre una seconda finestra **Query XML** contenente lo script XMLA che elabora la partizione.  
  
8.  Nella finestra di dialogo **Elabora partizione** fare clic su **Annulla** per chiudere l'editor.  
  
     In questa fase è necessario unire i due script e assicurarsi che la dimensione venga elaborata per prima.  
  
    > [!WARNING]  
    >  Se la partizione viene elaborata per prima, la successiva elaborazione della dimensione farà sì che la partizione rimanga in uno stato non elaborato. La partizione richiederebbe quindi una seconda elaborazione per raggiungere uno stato elaborato.  
  
9. Nella finestra **Query XMLA** contenente lo script XMLA che elabora la partizione selezionare il codice all'interno dei tag `Batch` e `Parallel` , fare clic con il pulsante destro del mouse su tale script e scegliere **Copia**.  
  
    ```  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID> Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
    ```  
  
10. Aprire la finestra **Query XMLA** contenente lo script XMLA che elabora la dimensione. Fare clic con il pulsante destro del mouse all'interno dello script a sinistra del tag `</Process>` e scegliere **Incolla**.  
  
     Nell'esempio seguente viene illustrato lo script XMLA modificato.  
  
    ```  
    <Batch xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Customer</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
11. Selezionare lo script XMLA modificato, fare clic con il pulsante destro del mouse su tale script e scegliere **Copia**.  
  
12. In questo passaggio lo script XMLA viene copiato negli Appunti di Windows. È possibile lasciare lo script XMLA negli Appunti, salvarlo su un file o incollarlo nel Blocco note o un altro editor di testo.  
  
###  <a name="bkmk_Scheduling"></a> Creare e pianificare il processo di elaborazione batch  
  
1.  Connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e quindi aprire Esplora oggetti.  
  
2.  Espandere **SQL Server Agent**. Avviare il servizio, se non è già in esecuzione.  
  
3.  Fare clic con il pulsante destro del mouse su **Processi** e selezionare **Nuovo processo**.  
  
4.  Nella finestra di dialogo **Nuovo processo** immettere il nome del processo nella casella **Nome**.  
  
5.  In **Passaggi**fare clic su **Nuovo**.  
  
6.  Nella finestra di dialogo **Nuovo passaggio di processo** immettere il nome del passaggio nella casella **Nome passaggio**.  
  
7.  In **Tipo**selezionare **Comando di SQL Server Analysis Services**.  
  
8.  In **Esegui come**selezionare **Account del servizio SQL Server Agent**. Tenere presente, secondo quanto indicato nella sezione Prerequisiti, che questo account deve disporre di autorizzazioni amministrative su Analysis Services.  
  
9. In **Server**specificare il nome del server dell'istanza di Analysis Services.  
  
10. In **Comando**fare clic con il pulsante destro del mouse e scegliere **Incolla**.  
  
11. Fare clic su **OK**.  
  
12. Nella pagina **Pianificazioni** fare clic su **Nuova**.  
  
13. Nella finestra di dialogo **Nuova pianificazione processo** immettere il nome della pianificazione nella casella **Nome**e fare clic su **OK**.  
  
     In questo passaggio viene creata una pianificazione per domenica alle 12.00 AM. Nel passaggio successivo verrà illustrato come eseguire manualmente il processo. È inoltre possibile selezionare una pianificazione che eseguirà il processo mentre viene monitorato.  
  
14. Scegliere **OK** per chiudere la finestra di dialogo.  
  
15. In **Esplora oggetti**espandere **Processi**, fare clic con il pulsante destro del mouse sul processo creato e scegliere **Inizia processo al passaggio**.  
  
     Poiché il processo include un solo passaggio, verrà eseguito immediatamente. Se il processo è costituito da più di un passaggio, è possibile selezionare quello da cui dovrà iniziare il processo.  
  
16. Al termine del processo fare clic su **Chiudi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](../multidimensional-models/processing-options-and-settings-analysis-services.md)   
 [Creare script per le attività amministrative in Analysis Services](../script-administrative-tasks-in-analysis-services.md)  
  
  
