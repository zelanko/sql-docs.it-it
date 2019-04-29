---
title: Editor attività di monitoraggio eventi WMI (pagina Opzioni WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmieventwatcher.wmiquery.f1
helpviewer_keywords:
- WMI Event Watcher Task Editor
ms.assetid: 525f3de7-a021-4e52-9939-3a83c88f131a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8c3286d1246efb8b5ae2e17cf8df5d38d865a9f9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877682"
---
# <a name="wmi-event-watcher-task-editor-wmi-options-page"></a>Editor attività Monitoraggio eventi WMI (pagina Opzioni WMI)
  Usare la pagina **Opzioni WMI** della finestra di dialogo **Editor attività Monitoraggio eventi WM** per specificare l'origine della query WQL e la modalità di risposta dell'attività Monitoraggio eventi WMI agli eventi del servizio Strumentazione Gestione Windows (WMI).  
  
 Per ulteriori informazioni su questa attività, vedere [WMI Event Watcher Task](control-flow/wmi-event-watcher-task.md). Per altre informazioni su WQL (WMI Query Language), vedere l'argomento relativo a WMI (Windows Management Instrumentation) " [Query con WQL](https://go.microsoft.com/fwlink/?LinkId=79045)" in MSDN Library.  
  
## <a name="static-options"></a>Opzioni statiche  
 **WMIConnectionName**  
 Selezionare una gestione connessione WMI nell'elenco o creare una nuova gestione connessione facendo clic su \<**Nuova connessione WMI**>.  
  
 **Argomenti correlati:** [Gestione connessione WMI](connection-manager/wmi-connection-manager.md), [Editor gestione connessione WMI](../../2014/integration-services/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Consente di selezionare il tipo di origine della query WQL eseguita dall'attività. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su una query WQL. Selezionando questo valore viene visualizzata l'opzione dinamica **WQLQuerySource**.|  
|**Connessione file**|Consente di selezionare un file contenente la query WQL. Selezionando questo valore viene visualizzata l'opzione dinamica **WQLQuerySource**.|  
|**Variabile**|Consente di impostare l'origine su una variabile che definisce la query WQL. Selezionando questo valore viene visualizzata l'opzione dinamica **WQLQuerySource**.|  
  
 **ActionAtEvent**  
 Consente di specificare se l'evento WMI registra l'evento e inizia un'azione [!INCLUDE[ssIS](../includes/ssis-md.md)] oppure se si limita a registrare l'evento.  
  
 **AfterEvent**  
 Consente di specificare se l'attività ha esito positivo o negativo dopo avere ricevuto l'evento WMI oppure se deve continuare a monitorare l'evento per controllare se viene generato nuovamente.  
  
 **ActionAtTimeout**  
 Consente di specificare se l'attività registra un timeout della query WMI e inizia un evento [!INCLUDE[ssIS](../includes/ssis-md.md)] in risposta oppure se si limita a registrare il timeout.  
  
 **AfterTimeout**  
 Consente di specificare se l'attività ha esito positivo o negativo in risposta a un timeout oppure se deve continuare il monitoraggio per controllare se viene generato un altro timeout.  
  
 **NumberOfEvents**  
 Consente di specificare il numero di eventi da monitorare.  
  
 **Timeout**  
 Consente di specificare il numero di secondi di attesa per la generazione dell'evento. Un valore pari a 0 significa che non è attivo alcun timeout.  
  
## <a name="wqlquerysource-dynamic-options"></a>Opzioni dinamiche di WQLQuerySource  
  
### <a name="wqlquerysource--direct-input"></a>WQLQuerySource = Input diretto  
 **WQLQuerySource**  
 Consente di specificare una query o di immettere una query nella finestra di dialogo **Query WQL** visualizzata facendo clic sul pulsante (...).  
  
### <a name="wqlquerysource--file-connection"></a>WQLQuerySource = Connessione file  
 **WQLQuerySource**  
 Selezionare una gestione connessione file nell'elenco o fare clic su \<**Nuova connessione**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [Gestione connessione file](connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="wqlquerysource--variable"></a>WQLQuerySource = Variabile  
 **WQLQuerySource**  
 Selezionare una variabile nell'elenco oppure fare clic su \<**Nuova variabile**> per crearne una nuova.  
  
 **Argomenti correlati:** [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Aggiungere una variabile](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Monitoraggio eventi WMI &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Pagina Espressioni](expressions/expressions-page.md)   
 [Attività Lettore di dati WMI](control-flow/wmi-data-reader-task.md)  
  
  
