---
title: Attività Lettore di dati WMI | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmidatareadertask.f1
- sql13.dts.designer.wmidatareadertask.general.f1
- sql13.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Data Reader task [Integration Services]
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fa4eca66eaab6abf6b6bf4332dce1c48bb5835cd
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727308"
---
# <a name="wmi-data-reader-task"></a>Attività Lettore di dati WMI

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  L'attività Lettore di dati WMI esegue query che utilizzano il linguaggio di query di WMI (Windows Management Instrumentation, Strumentazione gestione Windows) per ottenere da WMI informazioni su un sistema informatico. È possibile utilizzare l'attività Lettore di dati WMI per gli scopi seguenti:  
  
-   Eseguire query sul registro eventi di Windows di un computer locale o remoto e scrivere le informazioni ottenute in un file o in una variabile.  
  
-   Ottenere informazioni sulla presenza, lo stato o le proprietà dei componenti hardware e quindi utilizzare tali informazioni per determinare se altre attività nel flusso di controllo devono essere eseguite o meno.  
  
-   Ottenere un elenco di applicazioni e determinare le versioni installate.  
  
 Per configurare l'attività Lettore di dati WMI, procedere nel modo seguente:  
  
-   Specificare la gestione connessione WMI da utilizzare.  
  
-   Specificare l'origine della query WQL. La query può essere archiviata in una proprietà dell'attività o all'esterno dell'attività, in una variabile o in un file.  
  
-   Definire il formato dei risultati della query WQL. L'attività supporta le tabelle, le coppie nome/valore delle proprietà e i valori di proprietà.  
  
-   Specificare la destinazione della query, che può essere costituita da una variabile o da un file.  
  
-   Indicare se la destinazione della query verrà sovrascritta o mantenuta oppure se i nuovi dati verranno accodati a quelli esistenti.  
  
 Se la destinazione è un file, l'attività Lettore di dati WMI utilizzerà una gestione connessione file per connettersi al file. Per ulteriori informazioni, vedere [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 L'attività Lettore di dati WMI utilizza una gestione connessione WMI per connettersi al server da cui legge le informazioni di WMI. Per altre informazioni, vedere [Gestione connessione WMI](../../integration-services/connection-manager/wmi-connection-manager.md).  
  
## <a name="wql-query"></a>Query WQL  
 WQL è un sottolinguaggio di SQL che include estensioni per supportare la notifica degli eventi WMI e altre caratteristiche specifiche di WMI. Per altre informazioni su WQL, vedere la documentazione di Strumentazione gestione Windows in [MSDN Library](https://go.microsoft.com/fwlink/?linkid=7022).  
  
> [!NOTE]  
>  Le classi WMI variano a seconda della versione di Windows.  
  
 La query WQL seguente restituisce le voci contenute nel registro eventi applicazioni.  
  
```  
SELECT * FROM Win32_NTLogEvent WHERE LogFile = 'Application' AND (SourceName='SQLISService' OR SourceName='SQLISPackage') AND TimeGenerated > '20050117'  
```  
  
 La query WQL seguente restituisce informazioni sui dischi logici.  
  
```  
SELECT FreeSpace, DeviceId, Size, SystemName, Description FROM Win32_LlogicalDisk  
```  
  
 La query WQL seguente restituisce un elenco degli aggiornamenti QFE (Quick Fix Engineering) applicati al sistema operativo.  
  
```  
Select * FROM Win32_QuickFixEngineering  
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-data-reader-task"></a>Messaggi di registrazione personalizzati disponibili nell'attività Lettore di dati WMI  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Lettore di dati WMI. Per altre informazioni, vedere [registrazione di Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|Indica che l'attività ha iniziato a leggere dati WMI.|  
|**WMIDataReaderOperation**|Specifica la query WQL eseguita dall'attività.|  
  
## <a name="configuration-of-the-wmi-data-reader-task"></a>Configurazione dell'attività Lettore di dati WMI  
 È possibile impostare le proprietà a livello di programmazione o tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Per informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Pagina Espressioni](../../integration-services/expressions/expressions-page.md)  
  
 Per informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="wmi-data-reader-task-editor-general-page"></a>Editor attività Lettore di dati WMI (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo **Editor attività Lettore di dati WMI** per assegnare un nome e una descrizione all'attività Lettore di dati WMI.  
  
  Per altre informazioni su WQL (WMI Query Language), vedere l'argomento relativo a WMI (Windows Management Instrumentation) [Query con WQL](https://go.microsoft.com/fwlink/?LinkId=79045)in MSDN Library.  
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare un nome univoco per l'attività Lettore di dati WMI. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Lettore di dati WMI.  
  
## <a name="wmi-data-reader-task-editor-wmi-options-page"></a>Editor attività Lettore di dati WMI (pagina Opzioni WMI)
  Usare la pagina **Opzioni WMI** della finestra di dialogo **Editor attività Lettore di dati WMI** per specificare l'origine della query WQL (Windows Management Instrumentation Query Language) e la destinazione del risultato della query.  
  
 Per altre informazioni su WQL (WMI Query Language), vedere l'argomento relativo a WMI (Windows Management Instrumentation) [Query con WQL](https://go.microsoft.com/fwlink/?LinkId=79045)in MSDN Library.  
  
### <a name="static-options"></a>Opzioni statiche  
 **WMIConnectionName**  
 Selezionare una gestione connessione WMI nell'elenco o creare una nuova gestione connessione facendo clic su \<**Nuova connessione WMI**>.  
  
 **Argomenti correlati:** [Gestione connessione WMI](../../integration-services/connection-manager/wmi-connection-manager.md), [Editor gestione connessione WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Consente di selezionare il tipo di origine della query WQL eseguita dall'attività. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su una query WQL. Selezionando questo valore viene visualizzata l'opzione dinamica **WQLQuerySourceType**.|  
|**Connessione file**|Consente di selezionare un file contenente la query WQL. Selezionando questo valore viene visualizzata l'opzione dinamica **WQLQuerySourceType**.|  
|**Variabile**|Consente di impostare l'origine su una variabile che definisce la query WQL. Selezionando questo valore viene visualizzata l'opzione dinamica **WQLQuerySourceType**.|  
  
 **OutputType**  
 Consente di specificare se l'output deve essere una tabella di dati, un valore di proprietà o un nome e valore di proprietà.  
  
 **OverwriteDestination**  
 Consente di specificare se mantenere, sovrascrivere o accodare ai dati originali nel file o nella variabile di destinazione.  
  
 **DestinationType**  
 Consente di selezionare il tipo di destinazione della query WQL eseguita dall'attività. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Connessione file**|Selezionare un file in cui salvare i risultati della query WQL. Selezionando questo valore viene visualizzata l'opzione dinamica **DestinationType**.|  
|**Variabile**|Impostare la variabile in cui archiviare i risultati della query WQL. Selezionando questo valore viene visualizzata l'opzione dinamica **DestinationType**.|  
  
### <a name="wqlquerysourcetype-dynamic-options"></a>Opzioni dinamiche di WQLQuerySourceType  
  
#### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = Input diretto  
 **WQLQuerySource**  
 Consente di specificare una query o di immettere una query nella finestra di dialogo **Query WQL** visualizzata facendo clic sul pulsante con i puntini di sospensione (...).  
  
#### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = Connessione file  
 **WQLQuerySource**  
 Selezionare una gestione connessione file nell'elenco o fare clic su \<**Nuova connessione**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [Gestione connessione file](../../integration-services/connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = Variabile  
 **WQLQuerySource**  
 Selezionare una variabile nell'elenco oppure fare clic su \<**Nuova variabile**> per crearne una nuova.  
  
 **Argomenti correlati:** [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Aggiungere una variabile](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
### <a name="destinationtype-dynamic-options"></a>Opzioni dinamiche di DestinationType  
  
#### <a name="destinationtype--file-connection"></a>DestinationType = Connessione file  
 **Destinazione**  
 Selezionare una gestione connessione file nell'elenco o fare clic su \<**Nuova connessione**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [Gestione connessione file](../../integration-services/connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="destinationtype--variable"></a>DestinationType = Variabile  
 **Destinazione**  
 Selezionare una variabile nell'elenco oppure fare clic su \<**Nuova variabile**> per crearne una nuova.  
  
 **Argomenti correlati:** [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Aggiungere una variabile](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flusso di controllo](../../integration-services/control-flow/control-flow.md)  
  
  
