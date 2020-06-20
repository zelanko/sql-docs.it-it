---
title: Distribuire ed eseguire pacchetti SSIS tramite stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 60914b0c-1f65-45f8-8132-0ca331749fcc
author: janinezhang
ms.author: janinez
ms.openlocfilehash: af4efe24c58d22738e0e7b38ca68f37ce29603f2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84951791"
---
# <a name="deploy-and-execute-ssis-packages-using-stored-procedures"></a>Distribuire ed eseguire pacchetti SSIS utilizzando le stored procedure
  Quando un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] viene configurato in modo da utilizzare il relativo modello di distribuzione, è possibile utilizzare le stored procedure nel catalogo di [!INCLUDE[ssIS](../includes/ssis-md.md)] per distribuire il progetto ed eseguire i pacchetti. Per informazioni sui modelli di distribuzione di progetti, vedere [Distribuzione di progetti e pacchetti](packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 Per distribuire il progetto ed eseguire i pacchetti, è inoltre possibile utilizzare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] . Per altre informazioni, vedere gli argomenti nella sezione **Vedere anche** .  
  
> [!TIP]
>  Ad eccezione di catalog.deploy_project, è possibile generare facilmente le istruzioni Transact-SQL per le stored procedure elencate nella procedura descritta di seguito effettuando le operazioni seguenti:  
> 
>  1.  In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]espandere il nodo **Cataloghi di Integration Services** in Esplora oggetti e selezionare il pacchetto che si desidera eseguire.  
> 2.  Fare clic con il pulsante destro del mouse sul pacchetto, quindi scegliere **Esegui**.  
> 3.  In base alle esigenze, impostare i valori dei parametri, le proprietà di gestione connessione e le opzioni nella scheda **Avanzate** , ad esempio il livello di registrazione.  
> 
>      Per altre informazioni sui livelli di registrazione, vedere [Abilitare la registrazione per l'esecuzione di pacchetti nel server SSIS](../../2014/integration-services/enable-logging-for-package-execution-on-the-ssis-server.md).  
> 4.  Prima di fare clic su **OK** per eseguire il pacchetto, scegliere **Script**. Transact-SQL viene visualizzato in una finestra dell'editor di query in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
## <a name="to-deploy-and-execute-a-package-using-stored-procedures"></a>Per distribuire ed eseguire un pacchetto utilizzando le stored procedure  
  
1.  Chiamare [catalog.deploy_project &#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database) per distribuire il progetto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto sul server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
     Per recuperare il contenuto binario del [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] file di distribuzione del progetto, per il parametro * \@ project_stream* usare un'istruzione SELECT con la funzione OPENROWSET e il provider bulk per set di righe. Questo provider consente di leggere i dati da un file. Tramite l'argomento SINGLE_BLOB per il provider BULK per set di righe, il contenuto del file di dati viene restituito come un set di righe a riga e colonna singole di tipo varbinary(max). Per altre informazioni, vedere [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
     Nell'esempio seguente, il progetto SSISPackages_ProjectDeployment viene distribuito nella cartella di pacchetti SSIS nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . I dati binari vengono letti dal file di progetto (SSISPackage_ProjectDeployment. ispac) e vengono archiviati nel parametro * \@ ProjectBinary* di tipo varbinary (max). Il valore del parametro * \@ ProjectBinary* viene assegnato al parametro * \@ project_stream* .  
  
    ```  
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  Chiamare [catalog.create_execution &#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) per creare un'istanza di esecuzione del pacchetto e chiamare facoltativamente [catalog.set_execution_parameter_value &#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) per impostare i valori del parametro di runtime.  
  
     Nell'esempio seguente, tramite catalog.create_execution viene creata un'istanza di esecuzione per package.dtsx che è contenuto nel progetto SSISPackage_ProjectDeployment. Il progetto si trova nella cartella di pacchetti SSIS. Il valore di execution_id restituito dalla stored procedure viene utilizzato per la chiamata a catalog.set_execution_parameter_value. Tramite questa seconda stored procedure il parametro LOGGING_LEVEL viene impostato su 3 (registrazione dettagliata) e un parametro del pacchetto denominato Parameter1 viene impostato su un valore 1.  
  
     Per i parametri come LOGGING_LEVEL, il valore di object_type è 50. Per i parametri del pacchetto, il valore di object_type è 30.  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  Chiamare [catalog.start_execution &#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) per eseguire il pacchetto.  
  
     Nell'esempio seguente, una chiamata a catalog.start_execution viene aggiunta a Transact-SQL per avviare l'esecuzione del pacchetto. Viene utilizzato il valore di execution_id restituito dalla stored procedure catalog.create_execution.  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    EXEC [SSISDB].[catalog].[start_execution] @execution_id  
    GO  
  
    ```  
  
## <a name="to-deploy-a-project-from-server-to-server-using-stored-procedures"></a>Per distribuire un progetto da un server in un altro mediante stored procedure  
 È possibile distribuire un progetto da server a server tramite le stored procedure [catalog.get_project &#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database) e [catalog.deploy_project &#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database).  
  
 Prima di eseguire le stored procedure, è necessario effettuare le operazioni riportate di seguito.  
  
-   Creare un oggetto server collegato. Per altre informazioni, vedere [Creare server collegati &#40;Motore di database di SQL Server&#41;](../database-engine/sql-server-database-engine-overview.md).  
  
     Nella pagina **Opzioni server** della finestra di dialogo **Proprietà server collegato** impostare **RPC** e **RPC Out** su **True**. Impostare anche **Abilita innalzamento di livello delle transazioni distribuite per RPC** su **False**.  
  
-   Abilitare i parametri dinamici per il provider selezionato per il server collegato espandendo il nodo **Provider** in **Server collegati** in Esplora oggetti, facendo clic con il pulsante destro del mouse sul provider e selezionando **Proprietà**. Selezionare **Abilita** accanto a **Parametro dinamico**.  
  
-   Verificare che Distributed Transaction Coordinator (DTC) venga avviato in entrambi i server.  
  
 Chiamare catalog.get_project per restituire i dati binari per il progetto, quindi chiamare catalog.deploy_project. Il valore restituito da catalog.get_project viene inserito in una variabile di tabella di tipo varbinary(max). Tramite il server collegato non possono essere restituiti risultati di tipo varbinary(max).  
  
 Nell'esempio seguente, tramite catalog.get_project viene restituito un file binario per il progetto SSISPackages nel server collegato. Tramite catalog.deploy_project il progetto viene distribuito nella cartella denominata DestFolder nel server locale.  
  
```  
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuire progetti nel server Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [Eseguire un pacchetto in SQL Server Data Tools](../../2014/integration-services/run-a-package-in-sql-server-data-tools.md)   
 [Eseguire un pacchetto sul server SSIS mediante SQL Server Management Studio](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
  
