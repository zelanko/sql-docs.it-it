---
title: Opzioni di Richiesta profilo Inclusione valore (Attività Profiling dati) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: ca94da82-a4c9-4e87-9cba-c2d85bd31f01
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0bebe29e50ad4adaa6152eaef17de64a926433c8
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913831"
---
# <a name="value-inclusion-profile-request-options-data-profiling-task"></a>Opzioni di Richiesta profilo Inclusione valore (Attività Profiling dati)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Usare il riquadro **Proprietà richiesta** della pagina **Richieste profilo** per impostare le opzioni per **Richiesta profilo Inclusione valore** selezionata nel riquadro delle richieste. Il profilo Inclusione valore calcola la sovrapposizione dei valori tra due colonne o set di colonne. Di conseguenza, il profilo può inoltre determinare se una colonna o un set di colonne è adatto per fungere da chiave esterna tra le tabelle selezionate. Questo profilo consente inoltre di identificare eventuali problemi nei dati, ad esempio valori non validi. È possibile utilizzare un profilo Inclusione valore, ad esempio, per analizzare la colonna ProductId di una tabella Sales. Il profilo individua che la colonna contiene valori non inclusi nella colonna ProductID della tabella Products.  
  
> [!NOTE]  
>  Le opzioni descritte in questo argomento vengono visualizzate nella pagina **Richieste profilo** in **Editor attività Profiling dati**. Per altre informazioni su questa pagina dell'editor, vedere [Editor attività Profiling dati &#40;pagina Richieste profilo&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Per altre informazioni su come usare l'attività Profiling dati, vedere [Impostazione dell'attività Profiling dati](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Per altre informazioni sull'uso del Visualizzatore profilo dati per analizzare l'output dell'attività Profiling dati, vedere [Visualizzatore profilo dati](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-columns-for-the-inclusioncolumns-property"></a>Informazioni sulla selezione di colonne per la proprietà InclusionColumns  
 La funzionalità **Richiesta profilo Inclusione valore** consente di determinare se tutti i valori inclusi in un subset sono presenti nel superset. Il superset è spesso una tabella di ricerca o di riferimento. La colonna contenente gli stati in una tabella di indirizzi, ad esempio, rappresenta la tabella del subset. Ogni codice di stato di due caratteri incluso in questa colonna deve essere presente anche nella tabella dei codici di stato del servizio postale degli Stati Uniti, che rappresenta la tabella del superset.  
  
 Quando si utilizza il carattere jolly (*) come valore per la colonna del subset o la colonna del superset, l'attività Profiling dati confronta ogni colonna sul lato specifico rispetto alla colonna definita sull'altro lato.  
  
> [!NOTE]  
>  Se si seleziona (*), questa opzione potrebbe comportare un numero elevato di calcoli, riducendo le prestazioni dell'attività.  
  
## <a name="understanding-the-threshold-settings"></a>Informazioni sulle impostazioni di soglia  
 È possibile utilizzare due impostazioni di soglia diverse per ridefinire l'output di una richiesta del profilo Inclusione valore.  
  
 Quando si specifica un valore diverso da **None** per **InclusionThresholdSetting**, il profilo segnala l'attendibilità dell'inclusione del subset nel superset solo in presenza di una delle condizioni seguenti:  
  
-   L'attendibilità dell'inclusione supera la soglia specificata in **InclusionStrengthThreshold**.  
  
-   L'attendibilità dell'inclusione ha un valore pari a 1,0 e la proprietà **InclusionStrengthThreshold** è impostata su **Exact**.  
  
 È possibile ridefinire ulteriormente l'output escludendo le combinazioni in cui la colonna del superset non è una chiave appropriata per la tabella del superset a causa di valori non univoci. Quando si specifica un valore diverso da **None** per **SupersetColumnsKeyThresholdSetting**, il profilo segnala l'attendibilità dell'inclusione del subset nel superset solo in presenza di una delle condizioni seguenti:  
  
-   L'idoneità delle colonne del superset come chiave nella tabella del superset supera la soglia specificata in **SupersetColumnsKeyThreshold**  
  
-   L'attendibilità dell'inclusione ha un valore pari a 1,0 e la proprietà **SupersetColumnsKeyThreshold** è impostata su **Exact**.  
  
## <a name="request-properties-options"></a>Opzioni del riquadro Proprietà richiesta  
 Per **Richiesta profilo Inclusione valore**nel riquadro **Proprietà richiesta** vengono visualizzati i gruppi di opzioni seguenti:  
  
-   **Dati**che include le opzioni **SubsetTableOrView**, **SupersetTableOrView**e **InclusionColumns**  
  
-   **Generale**  
  
-   **Opzioni**  
  
### <a name="data-options"></a>Opzioni dati  
 **ConnectionManager**  
 Consente di selezionare la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] esistente che usa il provider di dati .NET per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) ai fini della connessione al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente la tabella o la vista di cui eseguire il profiling.  
  
 **SubsetTableOrView**  
 Consente di selezionare la tabella o la vista esistente da analizzare.  
  
 Per ulteriori informazioni, vedere la sezione "Opzioni SubsetTableOrView e SupersetTableOrView" in questo argomento.  
  
 **SupersetTableOrView**  
 Consente di selezionare la tabella o la vista esistente da analizzare.  
  
 Per ulteriori informazioni, vedere la sezione "Opzioni SubsetTableOrView e SupersetTableOrView" in questo argomento.  
  
 **InclusionColumns**  
 Consente di selezionare la colonna o i set di colonne dalle tabelle del subset e del superset.  
  
 Per ulteriori informazioni, vedere le sezioni "Informazioni sulla selezione di colonne per la proprietà InclusionColumns" e "Opzioni InclusionColumns" in questo argomento.  
  
#### <a name="subsettableorview-and-supersettableorview-options"></a>Opzioni SubsetTableOrView e SupersetTableOrView  
 **Schema**  
 Specifica lo schema a cui appartiene la tabella selezionata. Questa opzione è di sola lettura.  
  
 **TableOrView**  
 Visualizza il nome della tabella selezionata. Questa opzione è di sola lettura.  
  
#### <a name="inclusioncolumns-options"></a>Opzioni InclusionColumns  
 Le opzioni seguenti sono disponibili per ogni set di colonne selezionato per l'analisi in **InclusionColumns**.  
  
 Per ulteriori informazioni, vedere la sezione "Informazioni sulla selezione di colonne per la proprietà InclusionColumns" riportata in precedenza in questo argomento.  
  
 **IsWildcard**  
 Specifica se è stato selezionato il carattere jolly **(\*)** . Questa opzione è impostata su **True** se è stato selezionato **(\*)** per profilare tutte le colonne. È impostata su **False** se è stata selezionata una singola colonna da analizzare. Questa opzione è di sola lettura.  
  
 **ColumnName**  
 Visualizza il nome della colonna selezionata. È vuota se è stato selezionato **(\*)** per profilare tutte le colonne. Questa opzione è di sola lettura.  
  
 **StringCompareOptions**  
 Consente di selezionare le opzioni per il confronto di valori stringa. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente. Il valore predefinito di questa opzione è **Default**.  
  
> [!NOTE]  
>  Quando si usa il carattere jolly **(\*)** per **ColumnName**, **CompareOptions** è di sola lettura ed è impostato su **Default**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Default**|Ordina e confronta i dati in base alle regole di confronto della colonna nella tabella di origine.|  
|**BinarySort**|Ordina e confronta i dati di in base ai modelli di bit definiti per ogni carattere. L'ordinamento binario supporta la distinzione tra maiuscole e minuscole e tra caratteri accentati e non accentati e rappresenta inoltre il tipo di ordinamento più rapido.|  
|**DictionarySort**|Ordina e confronta i dati in base alle regole di ordinamento e confronto definite nei dizionari per la lingua o l'alfabeto associato.|  
  
 Se si seleziona **DictionarySort**, è inoltre possibile selezionare qualsiasi combinazione delle opzioni elencate nella tabella seguente. Per impostazione predefinita, nessuna di queste opzioni aggiuntive è selezionata.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**IgnoreCase**|Specifica se nel confronto viene fatta distinzione tra lettere maiuscole e minuscole. Se questa opzione è impostata, nel confronto tra stringhe verrà ignorata la combinazione di maiuscole e minuscole. Ad esempio, la stringa "ABC" verrà considerata identica alla stringa "abc".|  
|**IgnoreNonSpace**|Specifica se nel confronto viene fatta distinzione tra i caratteri con spaziatura e quelli con segni diacritici. Se questa opzione è impostata, nel confronto verranno ignorati i segni diacritici. Ad esempio, il carattere "Ã¥" verrà considerato uguale al carattere "a".|  
|**IgnoreKanaType**|Specifica se nel confronto viene fatta distinzione tra i due tipi di caratteri Kana giapponesi, Hiragana e Katakana. Se questa opzione è impostata, nel confronto tra stringhe verrà ignorata la distinzione tra Katakana e Hiragana.|  
|**IgnoreWidth**|Specifica se nel confronto viene fatta distinzione tra un carattere a un byte (metà larghezza) e lo stesso carattere rappresentato con due byte (larghezza intera). Se questa opzione è impostata, nel confronto tra stringhe la rappresentazione a un byte e quella a due byte dello stesso carattere verranno considerate uguali.|  
  
### <a name="general-options"></a>Opzioni generali  
 **RequestID**  
 Nome descrittivo per identificare la richiesta di profilo. Non è in genere necessario modificare il valore generato automaticamente.  
  
### <a name="options"></a>Opzioni  
 **InclusionThresholdSetting**  
 Selezionare l'impostazione di soglia per ridefinire l'output del profilo. Il valore predefinito di questa proprietà è **Specified**. Per ulteriori informazioni, vedere la sezione "Informazioni sulle impostazioni di soglia" riportata in precedenza in questo argomento.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Nessuno**|Non specifica alcuna soglia. Il livello di attendibilità della chiave viene segnalato indipendentemente dal valore.|  
|**Specified**|Consente di usare la soglia specificata in **InclusionStrengthThreshold**. Il livello di attendibilità dell'inclusione viene segnalato solo se è maggiore della soglia.|  
|**Exact**|Non specifica alcuna soglia. Il livello di attendibilità dell'inclusione viene segnalato solo se i valori del subset sono inclusi completamente nei valori del superset.|  
  
 **InclusionStrengthThreshold**  
 Specifica la soglia (utilizzando un valore compreso tra 0 e 1) al di sopra della quale deve essere segnalato il livello di attendibilità dell'inclusione. Il valore predefinito di questa proprietà è 0.95. Questa opzione è attivata solo quando si seleziona **Specified** come **InclusionThresholdSetting**.  
  
 Per ulteriori informazioni, vedere la sezione "Informazioni sulle impostazioni di soglia" riportata in precedenza in questo argomento.  
  
 **SupersetColumnsKeyThresholdSetting**  
 Consente di specificare la soglia del superset. Il valore predefinito di questa proprietà è **Specified**. Per ulteriori informazioni, vedere la sezione "Informazioni sulle impostazioni di soglia" riportata in precedenza in questo argomento.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Nessuno**|Non specifica alcuna soglia. Il livello di attendibilità dell'inclusione viene segnalato indipendentemente dall'attendibilità della chiave nella colonna del superset.|  
|**Specified**|Consente di usare la soglia specificata in **SupersetColumnsKeyThreshold**. Il livello di attendibilità dell'inclusione viene segnalato solo se l'attendibilità della chiave nella colonna del superset è maggiore della soglia.|  
|**Exact**|Non specifica alcuna soglia. Il livello di attendibilità dell'inclusione viene segnalato solo se le colonne del superset rappresentano una chiave esatta nella colonna del superset.|  
  
 **SupersetColumnsKeyThreshold**  
 Specifica la soglia (utilizzando un valore compreso tra 0 e 1) al di sopra della quale deve essere segnalato il livello di attendibilità dell'inclusione. Il valore predefinito di questa proprietà è 0.95. Questa opzione è attivata solo quando si seleziona **Specified** come **SupersetColumnsKeyThresholdSetting**.  
  
 Per ulteriori informazioni, vedere la sezione "Informazioni sulle impostazioni di soglia" riportata in precedenza in questo argomento.  
  
 **MaxNumberOfViolations**  
 Specifica il numero massimo di violazioni di inclusione da segnalare nell'output. Il valore predefinito di questa proprietà è 100. Questa opzione è disabilitata quando si seleziona **Exact** come **InclusionThresholdSetting**.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor attività Profiling dati &#40;pagina Generale&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Form profilo rapido singola tabella &#40;Attività Profiling dati&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
