---
title: Tocchi del flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2d847adf-4b3d-4949-a195-ef43de275077
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 053b34add45354d0df71fa73a72f8786cc706d15
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432438"
---
# <a name="data-flow-taps"></a>Scelte del flusso di dati
  In [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] è stata introdotta una nuova funzionalità con cui è possibile aggiungere una scelta dei dati in un percorso del flusso di dati di un pacchetto in fase di esecuzione e indirizzare l'output della scelta dei dati a un file esterno. Per utilizzare questa funzionalità, è necessario distribuire il progetto SSIS utilizzando il modello di distribuzione del progetto in un server SSIS. Al termine della distribuzione del pacchetto nel server, è necessario eseguire script T-SQL nel database SSISDB per aggiungere le scelte dei dati prima dell'esecuzione del pacchetto. Di seguito è riportato uno scenario di esempio:  
  
1.  Creare un'istanza di esecuzione di un pacchetto usando la stored procedure [catalog.create_execution &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database).  
  
2.  Aggiungere una scelta dei dati usando la stored procedure [catalog.add_data_tap](/sql/integration-services/system-stored-procedures/catalog-add-data-tap) o [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid) .  
  
3.  Avviare l'istanza di esecuzione del pacchetto usando [catalog.start_execution &#40;databse SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database).  
  
 Di seguito è riportato uno script SQL di esempio tramite cui vengono eseguiti i passaggi descritti nello scenario sopra indicato:  
  
```  
  
Declare @execid bigint  
EXEC [SSISDB].[catalog].[create_execution] @folder_name=N'ETL Folder', @project_name=N'ETL Project', @package_name=N'Package.dtsx', @execution_id=@execid OUTPUT  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt'  
EXEC [SSISDB].[catalog].[start_execution] @execid  
  
```  
  
 I parametri del nome della cartella, del nome del progetto e del nome del pacchetto della stored procedure create_execution corrispondono ai nomi della cartella, del progetto e del pacchetto nel catalogo di Integration Services. È possibile ottenere i nomi della cartella, del progetto e del pacchetto da utilizzare nella chiamata a create_execution da SQL Server Management Studio come illustrato nella figura riportata di seguito. Se non viene visualizzato il progetto SSIS in questo punto, non può ancora essere distribuito nel server SSIS. Fare clic con il pulsante destro del mouse sul progetto SSIS in Visual Studio e scegliere Distribuisci per distribuire il progetto nel server SSIS previsto.  
  
 Anziché digitare le istruzioni SQL, è possibile generare lo script di esecuzione del pacchetto effettuando i passaggi seguenti:  
  
1.  Fare clic con il pulsante destro del mouse su **Package.dtsx** , quindi scegliere **Esegui**.  
  
2.  Fare clic sul pulsante della barra degli strumenti **Script** per generare lo script.  
  
3.  A questo punto, aggiungere l'istruzione add_data_tap prima della chiamata a start_execution.  
  
 Il parametro task_package_path della stored procedure add_data_tap corrisponde alla proprietà PackagePath dell'attività Flusso di dati in Visual Studio. In Visual Studio fare clic con il pulsante destro del mouse su **Attività Flusso di dati**e scegliere **Proprietà** per avviare la relativa finestra.  Prendere nota del valore della proprietà **PackagePath** per usarlo come valore per il parametro task_package_path per la chiamata della stored procedure add_data_tap.  
  
 Il parametro dataflow_path_id_string della stored procedure add_data_tap corrisponde alla proprietà IdentificationString del percorso del flusso di dati a cui si desidera aggiungere una scelta dei dati. Per ottenere dataflow_path_id_string, fare clic sul percorso del flusso di dati (la freccia tra le attività nel flusso di dati) e prendere nota del valore della proprietà **IdentificationString** nella finestra Proprietà.  
  
 Quando si esegue lo script, il file di output viene archiviato in \<Program Files> \Microsoft SQL Server\110\DTS\DataDumps. Se esiste già un file con il nome, viene creato un nuovo file con un suffisso, ad esempio output[1].txt.  
  
 Come accennato in precedenza, è inoltre possibile usare la stored procedure [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid)anziché la stored procedure add_data_tap. Questa stored procedure accetta l'ID dell'attività Flusso di dati come parametro anziché task_package_path. È possibile ottenere l'ID dell'attività Flusso di dati dalla finestra delle proprietà di Visual Studio.  
  
## <a name="removing-a-data-tap"></a>Rimozione di una scelta dei dati  
 È possibile rimuovere una scelta dei dati prima di avviare l'esecuzione usando la stored procedure [catalog.remove_data_tap](/sql/integration-services/system-stored-procedures/catalog-remove-data-tap) . Questa stored procedure accetta l'ID della scelta dei dati come parametro, che è possibile ottenere come output della stored procedure add_data_tap.  
  
```  
  
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
  
```  
  
## <a name="listing-all-data-taps"></a>Elenco di tutte le scelte dei dati  
 È inoltre possibile elencare tutte le scelte dei dati tramite la vista catalog.execution_data_taps. Nell'esempio seguente vengono estratte le scelte dei dati per un'istanza di esecuzione specifica (ID: 54).  
  
```  
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
## <a name="performance-consideration"></a>Considerazione sulle prestazioni  
 L'abilitazione del livello di registrazione dettagliata e l'aggiunta di scelte dei dati determinano un aumento delle operazioni di I/O eseguite dalla soluzione di integrazione dei dati. Pertanto, è consigliabile aggiungere le scelte dei dati solo ai fini della risoluzione dei problemi.  
  
## <a name="video"></a>Video  
 In questo [video su TechNet](https://technet.microsoft.com/sqlserver/dn600163) viene illustrato come aggiungere o usare le scelte dei dati nel catalogo di SQL Server 2012 SSISDB che facilita il debug dei pacchetti a livello di codice e l'acquisizione dei risultati parziali in fase di esecuzione. Inoltre vengono illustrate la modalità per elencare/rimuovere queste scelte dei dati e le procedure consigliate per l'utilizzo delle scelte dei dati nei pacchetti SSIS.  
  
## <a name="related-tasks"></a>Attività correlate  
 [Debug di un flusso di dati](troubleshooting/debugging-data-flow.md)  
  
 [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
