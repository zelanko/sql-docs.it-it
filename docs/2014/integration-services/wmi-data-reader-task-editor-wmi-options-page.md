---
title: Editor attività lettore di dati WMI (pagina Opzioni WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WMI Data Reader Task Editor
ms.assetid: 4b8d4716-882d-41b0-b77e-e0e2741a2cd5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8367f0ae57df5333808e4dfde25c5676a3bcf1d4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054362"
---
# <a name="wmi-data-reader-task-editor-wmi-options-page"></a>Editor attività Lettore di dati WMI (pagina Opzioni WMI)
  Usare la pagina **Opzioni WMI** della finestra di dialogo **Editor attività Lettore di dati WMI** per specificare l'origine della query WQL (Windows Management Instrumentation Query Language) e la destinazione del risultato della query.  
  
 Per ulteriori informazioni su questa attività, vedere [WMI Data Reader Task](control-flow/wmi-data-reader-task.md). Per altre informazioni su WQL (WMI Query Language), vedere l'argomento relativo a WMI (Windows Management Instrumentation) [Query con WQL](https://go.microsoft.com/fwlink/?LinkId=79045)in MSDN Library.  
  
## <a name="static-options"></a>Opzioni statiche  
 **WMIConnectionName**  
 Selezionare una gestione connessione WMI nell'elenco o creare una nuova gestione connessione facendo clic su \<**Nuova connessione WMI**>.  
  
 **Argomenti correlati:** [gestione connessione WMI](connection-manager/wmi-connection-manager.md), [Editor gestione connessione WMI](../../2014/integration-services/wmi-connection-manager-editor.md)  
  
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
  
## <a name="wqlquerysourcetype-dynamic-options"></a>Opzioni dinamiche di WQLQuerySourceType  
  
### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = Input diretto  
 **WQLQuerySource**  
 Consente di specificare una query o di immettere una query nella finestra di dialogo **Query WQL** visualizzata facendo clic sul pulsante con i puntini di sospensione (...).  
  
### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = Connessione file  
 **WQLQuerySource**  
 Selezionare una gestione connessione file nell'elenco oppure fare clic su \< **nuova connessione...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [gestione connessione file](connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = Variabile  
 **WQLQuerySource**  
 Selezionare una variabile nell'elenco oppure fare clic su \< **nuova variabile...**> per creare una nuova variabile.  
  
 **Argomenti correlati:** [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md)  
  
## <a name="destinationtype-dynamic-options"></a>Opzioni dinamiche di DestinationType  
  
### <a name="destinationtype--file-connection"></a>DestinationType = Connessione file  
 **Destinazione**  
 Selezionare una gestione connessione file nell'elenco oppure fare clic su \< **nuova connessione...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [gestione connessione file](connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="destinationtype--variable"></a>DestinationType = Variabile  
 **Destinazione**  
 Selezionare una variabile nell'elenco oppure fare clic su \< **nuova variabile...**> per creare una nuova variabile.  
  
 **Argomenti correlati:** [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività lettore di dati WMI &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Pagina Espressioni](expressions/expressions-page.md)   
 [Attività Monitoraggio eventi WMI](control-flow/wmi-event-watcher-task.md)  
  
  
