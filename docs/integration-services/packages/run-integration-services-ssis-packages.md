---
title: Eseguire pacchetti di Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageexecute.f1
- sql13.ssis.ssms.executepackage.f1
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b3f4bc730a7823dc40387520068688d3e7145023
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52395901"
---
# <a name="run-integration-services-ssis-packages"></a>Eseguire pacchetti di Integration Services (SSIS)
  Per eseguire un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], è possibile usare vari strumenti, a seconda della posizione in cui sono archiviati tali pacchetti. Gli strumenti sono descritti nella tabella seguente.  

> [!NOTE]
> In questo articolo viene illustrato come eseguire i pacchetti SSIS a livello generale e come eseguire i pacchetti in locale. È possibile eseguire i pacchetti SSIS anche nelle piattaforme seguenti:
> - **Cloud di Microsoft Azure**. Per altre informazioni, vedere [Migrazione lift-and-shift dei carichi di lavoro di SQL Server Integration Services nel cloud](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md) e [Eseguire un pacchetto SSIS in Azure](../lift-shift/ssis-azure-run-packages.md).
> - **Linux**. Per altre informazioni, vedere [Estrarre, trasformare e caricare i dati in Linux con SSIS](../../linux/sql-server-linux-migrate-ssis.md).
  
 Per archiviare un pacchetto nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è possibile utilizzare il modello di distribuzione del progetto per distribuire il progetto nel server. Per informazioni, vedere [Distribuire progetti e pacchetti di Integration Services (SSIS)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 Per archiviare un pacchetto nell'archivio pacchetti SSIS, nel database msdb o nel file system, è possibile utilizzare il modello di distribuzione del pacchetto. Per altre informazioni, vedere [Distribuzione del pacchetto legacy &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
|Strumento|Pacchetti archiviati nel server Integration Services|Pacchetti archiviati nell'archivio pacchetti SSIS o nel database msdb|Pacchetti archiviati nel file system, all'esterno del percorso che fa parte dell'archivio pacchetti SSIS|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|no|no<br /><br /> È tuttavia possibile aggiungere un pacchetto esistente a un progetto dall'archivio pacchetti di [!INCLUDE[ssIS](../../includes/ssis-md.md)] , in cui è incluso il database msdb. L'aggiunta di un pacchetto esistente al progetto comporta la creazione di una copia locale del pacchetto nel file system.|Sì|  
|**SQL Server Management Studio, quando si è connessi a un'istanza del motore di database in cui è ospitato il server Integration Services**<br /><br /> Per altre informazioni, vedere [Finestra di dialogo Esecuzione pacchetto](#execute_package_dialog)|Sì|no<br /><br /> È tuttavia possibile importare un pacchetto nel server da questi percorsi.|no<br /><br /> È tuttavia possibile importare un pacchetto nel server dal file system.|
|**SQL Server Management Studio, quando si è connessi a un'istanza del motore di database in cui è ospitato il server Integration Services abilitato come master di scalabilità orizzontale**<br /><br /> Per altre informazioni, vedere [Eseguire pacchetti nel servizio di scalabilità orizzontale](../../integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)|Sì|no|no|
|**SQL Server Management Studio, quando è connesso al servizio Integration Services che gestisce l'archivio pacchetti SSIS**|no|Sì|no<br /><br /> È tuttavia possibile importare un pacchetto nell'archivio pacchetti di [!INCLUDE[ssIS](../../includes/ssis-md.md)] dal file system.|  
|**dtexec**<br /><br /> Per altre informazioni, vedere [dtexec Utility](../../integration-services/packages/dtexec-utility.md).|Sì|Sì|Sì|  
|**dtexecui**<br /><br /> Per altre informazioni, vedere [Riferimento all’interfaccia utente dell’utilità di esecuzione pacchetti &#40;DtExecUI&#41;](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)|no|Sì|Sì|  
|**SQL Server Agent**<br /><br /> Per pianificare un pacchetto, è possibile utilizzare un processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.<br /><br /> Per altre informazioni, vedere [Processi di SQL Server Agent per i pacchetti](../../integration-services/packages/sql-server-agent-jobs-for-packages.md).|Sì|Sì|Sì|  
|**Stored procedure predefinita**<br /><br /> Per altre informazioni, vedere [catalog.start_execution &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)|Sì|no|no|  
|**API gestita, tramite tipi e membri dello spazio dei nomi**  <xref:Microsoft.SqlServer.Management.IntegrationServices>|Sì|no|no|  
|**API gestita, tramite tipi e membri dello spazio dei nomi**  <xref:Microsoft.SqlServer.Dts.Runtime>|Non attualmente|Sì|Sì|  

## <a name="execution-and-logging"></a>Esecuzione e registrazione  
 È possibile abilitare la registrazione per i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], nonché acquisire informazioni di run-time in file di log. Per altre informazioni, vedere [registrazione di Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
 Per monitorare i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che vengono distribuiti ed eseguiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], utilizzare i report delle operazioni. I report sono disponibili in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Report per il server Integration Services](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
## <a name="run-a-package-in-sql-server-data-tools"></a>Eseguire un pacchetto in SQL Server Data Tools
  I pacchetti vengono eseguiti in genere in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante lo sviluppo, il debug e il test di pacchetti. In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] l'esecuzione dei pacchetti è sempre immediata.  
  
 Durante l'esecuzione di un pacchetto, in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] viene visualizzato lo stato dell'esecuzione nella scheda **Stato** . È possibile visualizzare l'ora di inizio e di fine del pacchetto e delle attività e contenitori del pacchetto, oltre a informazioni sulle attività o contenitori che hanno avuto esito negativo. Dopo l'esecuzione del pacchetto, nella scheda **Risultati esecuzione** sono disponibili le informazioni di run-time. Per altre informazioni, vedere la sezione "Report di stato" nell'argomento [Debug del flusso di controllo](../../integration-services/troubleshooting/debugging-control-flow.md).  
  
 **Distribuzione in fase di progettazione**. Quando si esegue un pacchetto in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], il pacchetto viene compilato e quindi distribuito in una cartella. Prima di eseguire il pacchetto è possibile specificare la cartella in cui deve essere distribuito. Se non si specifica alcuna cartella, per impostazione predefinita viene usata la cartella **bin** . Questo tipo di distribuzione è detto distribuzione in fase di progettazione.  
  
### <a name="to-run-a-package-in-sql-server-data-tools"></a>Per eseguire un pacchetto in SQL Server Data Tools  
  
1.  In Esplora soluzioni, se la soluzione contiene più progetti, fare clic con il pulsante destro del mouse sul progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contenente il pacchetto e quindi scegliere **Imposta come oggetto di avvio** per impostare il progetto di avvio.  
  
2.  In Esplora soluzioni, se il progetto contiene più pacchetti, fare clic con il pulsante destro del mouse su un pacchetto e quindi scegliere **Imposta come oggetto di avvio** per impostare il pacchetto di avvio.  
  
3.  Per eseguire un pacchetto, attenersi a una delle procedure seguenti:  
  
    -   Aprire il pacchetto da eseguire e quindi fare clic sul pulsante **Avvia debug** sulla barra dei menu oppure premere F5. Al termine dell'esecuzione del pacchetto premere MAIUSC+F5 per tornare alla modalità progettazione.  
  
    -   In Esplora soluzioni fare clic con il pulsante destro del mouse sul pacchetto e quindi scegliere **Esegui pacchetto**.  
  
### <a name="to-specify-a-different-folder-for-design-time-deployment"></a>Per specificare una cartella diversa per la distribuzione in fase di progettazione  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse sulla cartella del progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contenente il pacchetto da eseguire e quindi scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **\<Pagine delle proprietà di <nome progetto** fare clic su **Compila**.  
  
3.  Aggiornare il valore della proprietà OutputPath per specificare la cartella da usare per la distribuzione in fase di progettazione e quindi fare clic su **OK**.  


## <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>Eseguire un pacchetto sul server SSIS mediante SQL Server Management Studio
  Dopo aver distribuito il progetto nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è possibile eseguire il pacchetto nel server.  
  
 È possibile utilizzare i report relativi alle operazioni per visualizzare informazioni sui pacchetti eseguiti, o che sono attualmente in esecuzione, nel server. Per altre informazioni, vedere [Report per il server Integration Services](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>Per eseguire un pacchetto nel server mediante SQL Server Management Studio  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è contenuto il catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  In Esplora oggetti espandere il nodo **Cataloghi di Integration Services** , il nodo **SSISDB** e navigare al pacchetto contenuto nel progetto distribuito.  
  
3.  Fare clic con il pulsante destro del mouse sul nome del pacchetto e selezionare **Esegui**.  
  
4.  Configurare l'esecuzione del pacchetto usando le impostazioni sulle schede **Parametri**, **Gestioni connessioni**e **Avanzate** nella finestra di dialogo **Esegui pacchetto** .  
  
5.  Fare clic su **OK** per eseguire il pacchetto.  
  
     oppure  
  
     Utilizzare le stored procedure per eseguire il pacchetto. Fare clic su **Script** per generare l'istruzione Transact-SQL tramite cui viene creata e avviata un'istanza dell'esecuzione. Nell'istruzione è inclusa una chiamata alle stored procedure catalog.create_execution, catalog.set_execution_parameter_value e catalog.start_execution. Per altre informazioni su queste stored procedure, vedere [catalog.create_execution &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) e [catalog.start_execution &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).  

## <a name="execute_package_dialog"></a> Finestra di dialogo Esecuzione pacchetto
  Usare la finestra di dialogo **Esegui pacchetto** per eseguire un pacchetto archiviato nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 È possibile che in un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] siano contenuti i parametri con i valori archiviati nelle variabili di ambiente. Prima di eseguire tale pacchetto, è necessario specificare l'ambiente che sarà utilizzato per fornire i valori della variabile di ambiente. Un progetto può contenere più ambienti, ma solo un ambiente può essere utilizzato per l'associazione di valori della variabile di ambiente al momento dell'esecuzione. Se nel pacchetto non viene utilizzata alcuna variabile di ambiente, non sarà necessario alcun ambiente.  
  
 Per saperne di più  
  
-   [Aprire la finestra di dialogo Esegui pacchetto](#open_dialog)  
  
-   [Impostare le opzioni nella pagina Generale](#general)  
  
-   [Impostare le opzioni nella scheda Parametri](#parameters)  
  
-   [Impostare le opzioni nella scheda Gestioni connessioni](#connection)  
  
-   [Impostare le opzioni nella scheda Avanzate](#advanced)  
  
-   [Creazione di script per le opzioni contenute nella finestra di dialogo Esegui pacchetto](#script)  
  
###  <a name="open_dialog"></a> Aprire la finestra di dialogo Esegui pacchetto  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Verrà eseguita la connessione all'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in cui è ospitato il database SSISDB.  
  
2.  In Esplora oggetti espandere l'albero per visualizzare il nodo dei **cataloghi di Integration Services** .  
  
3.  Espandere il nodo **SSISDB** .  
  
4.  Espandere la cartella contenente il pacchetto che si desidera eseguire.  
  
5.  Fare clic con il pulsante destro del mouse sul pacchetto, quindi scegliere **Esegui**.  
  
###  <a name="general"></a> Impostare le opzioni nella pagina Generale  
 Selezionare **Ambiente** per specificare l'ambiente che viene applicato quando si esegue il pacchetto.  
  
###  <a name="parameters"></a> Impostare le opzioni nella scheda Parametri  
 Usare la scheda **Parametri** per modificare i valori dei parametri usati quando si esegue il pacchetto.  
  
###  <a name="connection"></a> Impostare le opzioni nella scheda Gestioni connessioni  
 Utilizzare la scheda Gestione connessioni per impostare le proprietà della gestione connessione del pacchetto.  
  
###  <a name="advanced"></a> Impostare le opzioni nella scheda Avanzate  
 Utilizzare la scheda Avanzate per gestire le proprietà e le altre impostazioni del pacchetto.  
  
 **Aggiungi**, **Modifica**, **Rimuovi**  
 Selezionare queste opzioni per aggiungere, modificare o rimuovere una proprietà.  
  
 **Livello di registrazione**  
 Consente di selezionare il livello di registrazione per l'esecuzione del pacchetto. Per altre informazioni, vedere [catalog.start_execution &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md).  
  
 **Dump su errori**  
 Specificare se creare un file di dump quando si verifica un errore durante l'esecuzione del pacchetto. Per altre informazioni, vedere [Generazione di file di dump per l'esecuzione del pacchetto](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
 **Runtime a 32 bit**  
 Specificare che il pacchetto verrà eseguito in un sistema a 32 bit.  
  
###  <a name="script"></a> Creazione di script per le opzioni contenute nella finestra di dialogo Esegui pacchetto  
 Mentre si è nella finestra di dialogo **Esegui pacchetto** , è inoltre possibile usare il pulsante **Script** nella barra degli strumenti per scrivere automaticamente codice [!INCLUDE[tsql](../../includes/tsql-md.md)] . Lo script generato chiama le stored procedure [catalog.start_execution &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) con le stesse opzioni selezionate nella finestra di dialogo **Esegui pacchetto**. Lo script verrà visualizzato in una nuova finestra dello script di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  

## <a name="see-also"></a>Vedere anche  
 [Utilità dtexec](../../integration-services/packages/dtexec-utility.md)   
[Avviare l'Importazione/Esportazione guidata SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  
