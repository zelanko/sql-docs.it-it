---
title: Opzioni di Richiesta profilo Chiave candidata (Attività Profiling dati) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 8632dbc4-4394-4dc7-b19c-f9adeb21ba52
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d682bacdc2bce10a118190108a2237419d4b9e27
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62832956"
---
# <a name="candidate-key-profile-request-options-data-profiling-task"></a>Opzioni di Richiesta profilo Chiave candidata (Attività Profiling dati)
  Usare il riquadro **Proprietà richiesta** della pagina **Richieste profilo** per impostare le opzioni di **Richiesta profilo Chiave candidata** selezionata nel riquadro delle richieste. Il profilo Chiave candidata segnala se una colonna o un set di colonne è una chiave o una chiave approssimativa per la tabella selezionata. Questo profilo consente inoltre di identificare eventuali problemi nei dati, ad esempio i valori duplicati in una possibile colonna chiave.  
  
> [!NOTE]  
>  Le opzioni descritte in questo argomento vengono visualizzate nella pagina **Richieste profilo** in **Editor attività Profiling dati**. Per altre informazioni su questa pagina dell'editor, vedere [Editor attività Profiling dati &#40;pagina Richieste profilo&#41;](data-profiling-task-editor-profile-requests-page.md).  
  
 Per altre informazioni su come usare l'attività Profiling dati, vedere [Impostazione dell'attività Profiling dati](data-profiling-task.md). Per altre informazioni sull'uso del Visualizzatore profilo dati per analizzare l'output dell'attività Profiling dati, vedere [Visualizzatore profilo dati](data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-columns-for-the-keycolumns-property"></a>Informazioni sulla selezione di colonne per la proprietà KeyColumns  
 La funzionalità **Richiesta profilo Chiave candidata** consente di calcolare il livello di attendibilità di una singola chiave candidata costituita da una o più colonne:  
  
-   Quando si seleziona solo una colonna in **KeyColumns**, l'attività calcola il livello di attendibilità della chiave di tale colonna.  
  
-   Quando si selezionano più colonne in **KeyColumns**, l'attività calcola il livello di attendibilità della chiave composta, che è costituita da tutte le colonne selezionate.  
  
-   Quando si seleziona il carattere jolly **(\*)** in **KeyColumns**, l'attività calcola il livello di attendibilità della chiave di ogni colonna nella tabella o nella vista.  
  
 Si consideri, ad esempio, una tabella di esempio contenente le colonne A, B e C. Per **KeyColumns**vengono selezionate le opzioni seguenti:  
  
-   Si seleziona (\*) e la colonna C in **KeyColumns**. L'attività calcola il livello di attendibilità della chiave della colonna C, quindi quella delle chiavi candidate composte (A,C) e (B, C).  
  
-   Si seleziona (\*) e (\*) in **KeyColumns**. L'attività calcola il livello di attendibilità della chiave delle singole colonne A, B e C, quindi delle chiavi candidate composte (A,B), (A,C) e (B, C).  
  
> [!NOTE]  
>  Se si seleziona (*), questa opzione potrebbe comportare un numero elevato di calcoli, riducendo le prestazioni dell'attività. Se l'attività, tuttavia, rileva un subset che soddisfa la soglia per una chiave, non vengono analizzate combinazioni aggiuntive. Se nella tabella di esempio descritta in precedenza, ad esempio, l'attività determina che la colonna C è una chiave, non verranno analizzate altre chiavi candidate composte.  
  
## <a name="request-properties-options"></a>Opzioni del riquadro Proprietà richiesta  
 Nel riquadro **Proprietà richiesta**per **Richiesta profilo Chiave candidata** vengono visualizzati i gruppi di opzioni seguenti:  
  
-   **Dati**che include le opzioni **TableOrView** e **KeyColumns**  
  
-   **Generale**  
  
-   **Opzioni**  
  
### <a name="data-options"></a>Opzioni dati  
 **ConnectionManager**  
 Consente di selezionare la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] esistente che usa il provider di dati .NET per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) ai fini della connessione al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente la tabella o la vista di cui eseguire il profiling.  
  
 **TableOrView**  
 Consente di selezionare la tabella o la vista esistente da analizzare.  
  
 Per ulteriori informazioni, vedere la sezione "Opzioni TableorView" in questo argomento.  
  
 **KeyColumns**  
 Consente di selezionare la colonna o le colonne da analizzare. Selezionare **(\*)** per analizzare tutte le colonne.  
  
 Per ulteriori informazioni, vedere le sezioni "Informazioni sulla selezione di colonne per la proprietà KeyColumns" e "Opzioni KeyColumns" in questo argomento.  
  
#### <a name="tableorview-options"></a>Opzioni TableOrView  
 **Schema**  
 Specifica lo schema a cui appartiene la tabella selezionata. Questa opzione è di sola lettura.  
  
 **Tabella**  
 Visualizza il nome della tabella selezionata. Questa opzione è di sola lettura.  
  
#### <a name="keycolumns-options"></a>Opzioni KeyColumns  
 Le opzioni seguenti sono disponibili per ogni colonna selezionata per l'analisi in **KeyColumns** o per l'opzione **(\*)** .  
  
 Per ulteriori informazioni, vedere la sezione "Informazioni sulla selezione di colonne per la proprietà KeyColumns" riportata in precedenza in questo argomento.  
  
 **IsWildcard**  
 Specifica se è stato selezionato il carattere jolly **(\*)** . Questa opzione è impostata su **True** se è stato selezionato **(\*)** per profilare tutte le colonne. È impostata su **False** se è stata selezionata una singola colonna da analizzare. Questa opzione è di sola lettura.  
  
 **ColumnName**  
 Visualizza il nome della colonna selezionata. È vuota se è stato selezionato **(\*)** per profilare tutte le colonne. Questa opzione è di sola lettura.  
  
 **StringCompareOptions**  
 Consente di selezionare le opzioni per il confronto di valori stringa. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente. Il valore predefinito di questa opzione è **Default**.  
  
> [!NOTE]  
>  Quando si usa il carattere jolly **(\*)** per **ColumnName**, la proprietà **CompareOptions** è di sola lettura ed è impostata su **Default**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Default**|Ordina e confronta i dati in base alle regole di confronto della colonna nella tabella di origine.|  
|**BinarySort**|Ordina e confronta i dati di in base ai modelli di bit definiti per ogni carattere. L'ordinamento binario supporta la distinzione tra maiuscole e minuscole e tra caratteri accentati e non accentati e rappresenta inoltre il tipo di ordinamento più rapido.|  
|**DictionarySort**|Ordina e confronta i dati in base alle regole di ordinamento e confronto definite nei dizionari per la lingua o l'alfabeto associato.|  
  
 Se si seleziona **DictionarySort**, è inoltre possibile selezionare qualsiasi combinazione delle opzioni elencate nella tabella seguente. Per impostazione predefinita, nessuna di queste opzioni aggiuntive è selezionata.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**IgnoreCase**|Specifica se nel confronto viene fatta distinzione tra lettere maiuscole e minuscole. Se questa opzione è impostata, nel confronto tra stringhe verrà ignorata la combinazione di maiuscole e minuscole. Ad esempio, la stringa "ABC" verrà considerata identica alla stringa "abc".|  
|**IgnoreNonSpace**|Specifica se nel confronto viene fatta distinzione tra i caratteri con spaziatura e quelli con segni diacritici. Se questa opzione è impostata, nel confronto verranno ignorati i segni diacritici. Ad esempio, il carattere "å" verrà considerato uguale al carattere "a".|  
|**IgnoreKanaType**|Specifica se nel confronto viene fatta distinzione tra i due tipi di caratteri Kana giapponesi, Hiragana e Katakana. Se questa opzione è impostata, nel confronto tra stringhe verrà ignorata la distinzione tra Katakana e Hiragana.|  
|**IgnoreWidth**|Specifica se nel confronto viene fatta distinzione tra un carattere a un byte (metà larghezza) e lo stesso carattere rappresentato con due byte (larghezza intera). Se questa opzione è impostata, nel confronto tra stringhe la rappresentazione a un byte e quella a due byte dello stesso carattere verranno considerate uguali.|  
  
### <a name="general-options"></a>Opzioni generali  
 **RequestID**  
 Nome descrittivo per identificare la richiesta di profilo. Non è in genere necessario modificare il valore generato automaticamente.  
  
### <a name="options"></a>Opzioni  
 **ThresholdSetting**  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente. Il valore predefinito di questa proprietà è **Specified**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Nessuno**|Non viene specificata alcuna soglia. Il livello di attendibilità della chiave viene segnalato indipendentemente dal valore.|  
|**Specified**|Viene specificata una soglia in **KeyStrengthThreshold**. Il livello di attendibilità della chiave viene segnalato solo se è maggiore della soglia.|  
|**Exact**|Non viene specificata alcuna soglia. Il livello di attendibilità della chiave viene segnalato solo se le colonne selezionate rappresentano una chiave esatta.|  
  
 **KeyStrengthThreshold**  
 Specifica la soglia (utilizzando un valore compreso tra 0 e 1) al di sopra della quale deve essere segnalato il livello di attendibilità della chiave. Il valore predefinito di questa proprietà è 0.95. Questa opzione è attivata solo quando si seleziona **Specified** come **KeyStrengthThresholdSetting**.  
  
 **MaxNumberOfViolations**  
 Specifica il numero massimo di violazioni della chiave candidata da segnalare nell'output. Il valore predefinito di questa proprietà è 100. Questa opzione è disabilitata quando si seleziona **Exact** come **KeyStrengthThresholdSetting**.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor attività Profiling dati &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)   
 [Form profilo rapido singola tabella &#40;Attività Profiling dati&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  
