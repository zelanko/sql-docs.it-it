---
title: Origine CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: af2f56c92947cd8e210b8532cb6899c52486707e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53349816"
---
# <a name="cdc-source"></a>Origine CDC
  Tramite l'origine CDC viene letto un intervallo di dati delle modifiche da tabelle delle modifiche di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ; queste vengono poi recapitate a valle ad altri componenti SSIS.  
  
 L'intervallo di dati delle modifiche letti dall'origine CDC è denominato intervallo di elaborazione CDC ed è determinato dall'attività di controllo CDC eseguita prima dell'inizio del flusso di dati corrente. L'Intervallo di elaborazione CDC viene derivato dal valore di una variabile del pacchetto che gestisce lo stato dell'elaborazione CDC per un gruppo di tabelle.  
  
 L'origine CDC estrae dati da un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite una tabella di database, una vista o un'istruzione SQL.  
  
 Per l'origine CDC vengono utilizzate le configurazioni seguenti:  
  
-   Una gestione connessione ADO.NET di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per accedere al database CDC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni sulla configurazione della connessione dell'origine CDC, vedere [CDC Source Editor &#40;Connection Manager Page&#41;](../cdc-source-editor-connection-manager-page.md).  
  
-   Una tabella abilitata per CDC.  
  
-   Il nome dell'istanza di acquisizione della tabella selezionata (se ne è presente più di una).  
  
-   La modalità di elaborazione delle modifiche.  
  
-   Il nome della variabile del pacchetto dello stato CDC in base alla quale viene determinato l'intervallo di elaborazione CDC. L'origine CDC non modifica questa variabile.  
  
 I dati restituiti dall'origine CDC sono identici a quelli restituiti dalle funzioni CDC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **cdc.fn_cdc_get_all_changes_\<capture-instance-name>** o **cdc.fn_cdc_get_net_changes_\<capture-instance-name>** (se disponibili). L'unica aggiunta facoltativa è la colonna **__$initial_processing** , che indica se l'intervallo di elaborazione corrente può essere sovrapposto a un caricamento iniziale della tabella. Per ulteriori informazioni sull'elaborazione iniziale, vedere [Attività di controllo CDC](../control-flow/cdc-control-task.md).  
  
 L'origine CDC include un output regolare e un output degli errori.  
  
## <a name="error-handling"></a>Gestione degli errori  
 L'origine CDC include un output degli errori. L'output degli errori del componente include le colonne di output seguenti:  
  
-   **Codice di errore**: Il valore è sempre -1.  
  
-   **Errore colonna**: La colonna di origine che provoca l'errore (per gli errori di conversione).  
  
-   **Error Row Columns**: I dati del record che ha provocato l'errore.  
  
 A seconda dell'impostazione del comportamento in seguito all'errore, l'origine CDC supporta la restituzione degli errori (conversione dei dati, troncamento) che si verificano durante il processo di estrazione nell'output degli errori. Per altre informazioni, vedere [CDC Source Editor &#40;Error Output Page&#41;](../cdc-source-editor-error-output-page.md).  
  
## <a name="data-type-support"></a>Supporto dei tipi di dati  
 Il componente di origine CDC per Microsoft supporta tutti i tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , di cui viene eseguito il mapping ai tipi di dati SSIS corretti.  
  
## <a name="troubleshooting-the-cdc-source"></a>Risoluzione dei problemi relativi all'origine CDC  
 Di seguito vengono fornite informazioni sulla risoluzione dei problemi relativi all'origine CDC.  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>Utilizzare questo script per isolare problemi e riprodurli in SQL Server Management Studio  
 Il funzionamento dell'origine CDC è regolato dal funzionamento dell'attività di controllo CDC eseguita prima di richiamare l'origine CDC. Tramite l'attività di controllo CDC viene preparato il valore della variabile del pacchetto dello stato CDC in modo da contenere gli LSN iniziale e finale. Viene eseguita la funzione equivalente allo script seguente:  
  
```  
use <cdc-enabled-database-name>  
               declare @start_lsn binary(10), @end_lsn binary(10)  
               set @start_lsn = sys.fn_cdc_increment_lsn(  
                       convert(binary(10),'0x' + '<value-from-state-cs>', 1))  
               set @end_lsn =   
                       convert(binary(10),'0x' + '<value-from-state-ce>', 1)  
               select * from cdc.fn_cdc_get_net_changes_dbo_Table1(@start_lsn,  
@end_lsn, '<mode>')  
```  
  
 dove:  
  
-   \<cdc-enabled-database-name> è il nome del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente le tabelle delle modifiche.  
  
-   \<value-from-state-cs> è il valore visualizzato nella variabile di stato CDC come CS/\<value-from-state-cs>/ (CS indica l'inizio dell'intervallo di elaborazione corrente).  
  
-   \<value-from-state-ce> è il valore visualizzato nella variabile di stato CDC come CE/\<value-from-state-cs>/ (CE indica la fine dell'intervallo di elaborazione corrente).  
  
-   \<mode> corrisponde alle modalità di elaborazione CDC. Le modalità di elaborazione hanno uno dei seguenti valori: **All**, **All with Old Values**, **Net**, **Net with Update Mask**, **Net with Merge**.  
  
 Questo script consente di isolare i problemi riproducendoli in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], in cui è possibile riprodurre e identificare facilmente gli errori.  
  
#### <a name="sql-server-error-message"></a>Messaggio di errore di SQL Server  
 È possibile che in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]venga restituito il messaggio di errore seguente:  
  
 **Numero di argomenti insufficiente per la routine o funzione cdc.fn_cdc_get_net_changes_\<.>.**  
  
 Questo errore non indica che un argomento è mancante. Indica invece che i valori LSN iniziale o finale nella variabile di stato CDC non sono validi.  
  
## <a name="configuring-the-cdc-source"></a>Configurazione dell'origine CDC  
 È possibile configurare l'origine CDC a livello di codice o tramite Progettazione SSIS.  
  
 Per ulteriori informazioni, vedere uno degli argomenti seguenti:  
  
-   [Editor origine CDC &#40;pagina Gestione connessione&#41;](../cdc-source-editor-connection-manager-page.md)  
  
-   [Editor origine CDC &#40;pagina Colonne&#41;](../cdc-source-editor-columns-page.md)  
  
-   [Editor origine CDC &#40;pagina Output degli errori&#41;](../cdc-source-editor-error-output-page.md)  
  
 La finestra di dialogo **Editor avanzato** contiene le proprietà che è possibile impostare a livello di codice.  
  
 Per aprire la finestra di dialogo **Editor avanzato** :  
  
-   Nella schermata **Flusso di dati** del progetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] fare clic con il pulsante destro del mouse sull'origine CDC e scegliere **Visualizza editor avanzato**.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** , vedere [Proprietà personalizzate dell'origine CDC](cdc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Editor origine CDC &#40;pagina Gestione connessione&#41;](../cdc-source-editor-connection-manager-page.md)  
  
-   [Editor origine CDC &#40;pagina Colonne&#41;](../cdc-source-editor-columns-page.md)  
  
-   [Editor origine CDC &#40;pagina Output degli errori&#41;](../cdc-source-editor-error-output-page.md)  
  
-   [Proprietà personalizzate dell'origine CDC](cdc-source-custom-properties.md)  
  
-   [Estrarre dati delle modifiche tramite l'origine CDC](cdc-source.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Intervento nel blog sulle [modalità di elaborazione per l'origine CDC](https://go.microsoft.com/fwlink/?LinkId=242541) sul sito Web mattmasson.com.  
  
  
