---
title: Abilitare la registrazione per l'esecuzione del pacchetto nel server SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d3e62f4c3b2549fbeac0302e7ea5d97a510bfc4a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966902"
---
# <a name="enable-logging-for-package-execution-on-the-ssis-server"></a>Abilitare la registrazione per l'esecuzione di pacchetti nel server SSIS
  In questa procedura viene descritto come impostare o modificare il livello di registrazione per un pacchetto quando si esegue un pacchetto che è stato distribuito al server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Il livello di registrazione impostato quando si esegue il pacchetto sovrascrive la registrazione del pacchetto configurata mediante [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Vedere [Abilitare la registrazione di pacchetti in SQL Server Data Tools](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md) per altre informazioni.  
  
 È possibile specificare il livello di registrazione utilizzando uno dei metodi indicati di seguito. In questo argomento viene illustrato il primo metodo.  
  
-   Configurazione di un'istanza di esecuzione di un pacchetto tramite la finestra di dialogo Esegui pacchetto  
  
-   Impostazione dei parametri per un'istanza di esecuzione usando il valore [catalog.set_execution_parameter_value &#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
  
-   Configurazione di un processo di SQL Server Agent per l'esecuzione di un pacchetto tramite la finestra di dialogo Nuovo passaggio di processo.  
  
### <a name="to-set-the-logging-level-for-a-package-by-using-the-execute-package-dialog-box"></a>Per impostare il livello di registrazione per un pacchetto mediante la finestra di dialogo Esegui pacchetto  
  
1.  In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], passare al pacchetto in Esplora oggetti.  
  
2.  Fare clic con il pulsante destro del mouse sul pacchetto e selezionare **Esegui**.  
  
3.  Selezionare la scheda **Avanzate** nella finestra di dialogo **Esecuzione pacchetto** .  
  
4.  In **Livello di registrazione**, selezionare il livello di registrazione. Per una descrizione dei valori disponibili, vedere la tabella di seguito.  
  
5.  Completare le eventuali altre configurazione pacchetto, quindi fare clic su **OK** per eseguire il pacchetto.  
  
 Sono disponibili i livelli di registrazione seguenti.  
  
|Livello di registrazione|Descrizione|  
|-------------------|-----------------|  
|nessuno|La registrazione è disabilitata. Solo lo stato dell'esecuzione del pacchetto viene registrato.|  
|Basic|Tutti gli eventi sono registrati, ad eccezione di eventi personalizzati e di diagnostica. Si tratta del valore predefinito.|  
|Prestazioni|Vengono registrati solo le statistiche sulle prestazioni e gli eventi OnError e OnWarning.<br /><br /> Nel report **Prestazioni di esecuzione** vengono visualizzati il tempo di attività e il tempo totale per i componenti flusso di dati del pacchetto. Queste informazioni sono disponibili se il livello di registrazione dell'ultima esecuzione del pacchetto è stato impostato su **Prestazioni** o **Dettagliato**. Per altre informazioni, vedere [report per il server Integration Services](../../2014/integration-services/reports-for-the-integration-services-server.md).<br /><br /> La vista [catalog.execution_component_phases](/sql/integration-services/system-views/catalog-execution-component-phases) visualizza le ore di inizio e di fine per i componenti flusso di dati, per ogni fase di esecuzione. In questa vista vengono visualizzate le informazioni per i componenti solo quando il livello di registrazione dell'esecuzione del pacchetto è impostato su **Prestazioni** o **Dettagliato**.|  
|Dettagliato|Tutti gli eventi vengono registrati, inclusi gli eventi personalizzati e di diagnostica.<br /><br /> L'evento DiagnosticEx rappresenta un esempio di un evento di diagnostica. Ogni volta che un'attività Esegui pacchetto esegue un pacchetto figlio, l'evento viene registrato. Il messaggio di evento include i valori dei parametri passati ai pacchetti figlio<br /><br /> Il valore della colonna di messaggio per DiagnosticEx è Testo XML. . Per visualizzare il testo del messaggio per l'esecuzione del pacchetto, eseguire una query nella vista [catalog.operation_messages &#40;database SSISDB&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database).<br /><br /> Nota: gli eventi personalizzati includono gli eventi registrati dalle [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] attività. Per ulteriori informazioni, vedere [la pagina relativa ai messaggi personalizzati per la registrazione](../../2014/integration-services/custom-messages-for-logging.md).<br /><br /> Nella vista [catalog.execution_data_statistics](../relational-databases/statistics/statistics.md) viene visualizzata una riga ogni volta che un componente flusso di dati invia dati a un componente downstream, per l'esecuzione di un pacchetto. Il livello di registrazione deve essere impostato su **Dettagliato** per acquisire queste informazioni nella vista.|  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services &#40;la registrazione&#41; SSIS](performance/integration-services-ssis-logging.md)   
 [Abilitare la registrazione di pacchetti in SQL Server Data Tools](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)  
  
  
