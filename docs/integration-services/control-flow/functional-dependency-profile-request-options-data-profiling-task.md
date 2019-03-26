---
title: Opzioni di Richiesta profilo Dipendenza funzionale (Attività Profiling dati) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 6eb853aa-8016-490c-be4f-06ab8d7f5021
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1ac20c9f13bbf39bc4ffd46cb6b036c8314684ca
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58274945"
---
# <a name="functional-dependency-profile-request-options-data-profiling-task"></a>Opzioni di Richiesta profilo Dipendenza funzionale (Attività Profiling dati)
  Usare il riquadro **Proprietà richiesta** della pagina **Richieste profilo** per impostare le opzioni di **Richiesta profilo Dipendenza funzionale** selezionata nel riquadro delle richieste. Un profilo Dipendenza funzionale segnala il livello di dipendenza dei valori inclusi in una colonna (colonna dipendente) dai valori presenti in un'altra colonna o set di colonne (colonna determinante). Questo profilo consente inoltre di identificare eventuali problemi nei dati, ad esempio valori non validi. Si analizza, ad esempio, la dipendenza tra una colonna che contiene i codici postali ZIP (Stati Uniti) e una colonna che contiene gli stati degli Stati Uniti. Benché nel profilo uno stesso codice postale debba essere sempre associato allo stesso stato, vengono individuate violazioni di tale dipendenza.  
  
> [!NOTE]  
>  Le opzioni descritte in questo argomento vengono visualizzate nella pagina **Richieste profilo** in **Editor attività Profiling dati**. Per altre informazioni su questa pagina dell'editor, vedere [Editor attività Profiling dati &#40;pagina Richieste profilo&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Per altre informazioni su come usare l'attività Profiling dati, vedere [Impostazione dell'attività Profiling dati](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Per altre informazioni sull'uso del Visualizzatore profilo dati per analizzare l'output dell'attività Profiling dati, vedere [Visualizzatore profilo dati](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-determinant-and-dependent-columns"></a>Informazioni sulla selezione di colonne determinanti e dipendenti  
 Una **Richiesta profilo Dipendenza funzionale** calcola il livello di determinazione del valore della colonna dipendente, specificata nella proprietà **DependentColumn** , da parte della colonna o del set di colonne determinanti, specificate nella proprietà **DeterminantColumns** . Tra una colonna che contiene gli stati degli Stati Uniti, ad esempio, e una colonna che contiene i codici postali ZIP (Stati Uniti) deve esistere una dipendenza funzionale. Ciò significa che se il codice postale ZIP (colonna determinante) è 98052, lo stato (colonna dipendente) deve essere sempre Washington.  
  
 Per il lato determinante, è possibile specificare una colonna o un set di colonne nella proprietà **DeterminantColumns** . Si consideri, ad esempio, una tabella di esempio contenente le colonne A, B e C. Per la proprietà **DeterminantColumns** vengono selezionate le opzioni seguenti:  
  
-   Quando si seleziona il carattere jolly **(\*)**, l'attività Profiling dati testa ogni colonna come lato determinante della dipendenza.  
  
-   Quando si selezionano il carattere jolly **(\*)** e un'altra colonna o colonne, l'attività Profiling dati testa ogni combinazione di colonne come lato determinante della dipendenza. Si consideri, ad esempio, una tabella di esempio contenente le colonne A, B e C. Se si specificano **(\*)** e la colonna C come valore della proprietà **DeterminantColumns**, l'attività Profiling dati testa le combinazioni (A, C) e (B, C) come lato determinante della dipendenza.  
  
 Per il lato dipendente, è possibile specificare una singola colonna o il carattere jolly **(\*)** nella proprietà **DependentColumn**. Quando si seleziona **(\*)**, l'attività Profiling dati testa la colonna o il set di colonne del lato determinante rispetto a ciascuna colonna.  
  
> [!NOTE]  
>  Se si seleziona **(\*)**, questa opzione potrebbe comportare un numero elevato di calcoli, riducendo le prestazioni dell'attività. Se l'attività, tuttavia, rileva un subset che soddisfa la soglia per una dipendenza funzionale, non vengono analizzate combinazioni aggiuntive. Nella tabella di esempio descritta in precedenza, ad esempio, se l'attività determina che la colonna C è una colonna determinante, non verranno analizzati altri candidati composti.  
  
## <a name="request-properties-options"></a>Opzioni del riquadro Proprietà richiesta  
 Nel riquadro **Proprietà richiesta**per **Richiesta profilo Dipendenza funzionale** vengono visualizzati i gruppi di opzioni seguenti:  
  
-   **Dati**che include le opzioni **DeterminantColumns** e **DependentColumn**  
  
-   **Generale**  
  
-   **Opzioni**  
  
### <a name="data-options"></a>Opzioni dati  
 **ConnectionManager**  
 Consente di selezionare la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] esistente che usa il provider di dati .NET per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) ai fini della connessione al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente la tabella o la vista di cui eseguire il profiling.  
  
 **TableOrView**  
 Consente di selezionare la tabella o la vista esistente da analizzare.  
  
 **DependentColumn**  
 Consente di selezionare la colonna o il set di colonne determinante. Consente pertanto di selezionare la colonna o il set di colonne i cui valori determinano il valore della colonna dipendente.  
  
 Per ulteriori informazioni, vedere le sezioni "Informazioni sulla selezione di colonne determinanti e dipendenti" e "Opzioni DeterminantColumns e DependentColumn" in questo argomento.  
  
 **DeterminantColumns**  
 Consente di selezionare la colonna dipendente. Consente pertanto di selezionare la colonna il cui valore è determinato dal valore della colonna o del set di colonne del lato determinante.  
  
 Per ulteriori informazioni, vedere le sezioni "Informazioni sulla selezione di colonne determinanti e dipendenti" e "Opzioni DeterminantColumns e DependentColumn" in questo argomento.  
  
#### <a name="determinantcolumns-and-dependentcolumn-options"></a>Opzioni DeterminantColumns e DependentColumn  
 Le opzioni seguenti sono disponibili per ogni colonna selezionata per l'analisi in **DeterminantColumns** e **DependentColumn**.  
  
 Per ulteriori informazioni, vedere la sezione "Informazioni sulla selezione di colonne determinanti e dipendenti" riportata in precedenza in questo argomento.  
  
 **IsWildCard**  
 Specifica se è stato selezionato il carattere jolly **(\*)**. Questa opzione è impostata su **True** se è stato selezionato **(\*)** per profilare tutte le colonne. È impostata su **False** se è stata selezionata una singola colonna da analizzare. Questa opzione è di sola lettura.  
  
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
|**IgnoreNonSpace**|Specifica se nel confronto viene fatta distinzione tra i caratteri con spaziatura e quelli con segni diacritici. Se questa opzione è impostata, nel confronto verranno ignorati i segni diacritici. Ad esempio, il carattere "å" verrà considerato uguale al carattere "a".|  
|**IgnoreKanaType**|Specifica se nel confronto viene fatta distinzione tra i due tipi di caratteri Kana giapponesi, Hiragana e Katakana. Se questa opzione è impostata, nel confronto tra stringhe verrà ignorata la distinzione tra Katakana e Hiragana.|  
|**IgnoreWidth**|Specifica se nel confronto viene fatta distinzione tra un carattere a un byte (metà larghezza) e lo stesso carattere rappresentato con due byte (larghezza intera). Se questa opzione è impostata, nel confronto tra stringhe la rappresentazione a un byte e quella a due byte dello stesso carattere verranno considerate uguali.|  
  
### <a name="general-options"></a>Opzioni generali  
 **RequestID**  
 Nome descrittivo per identificare la richiesta di profilo. Non è in genere necessario modificare il valore generato automaticamente.  
  
### <a name="options"></a>Opzioni  
 **ThresholdSetting**  
 Consente di specificare l'impostazione della soglia. Il valore predefinito di questa proprietà è **Specified**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**None**|Non specifica alcuna soglia. Il livello di attendibilità della dipendenza funzionale viene segnalato indipendentemente dal valore.|  
|**Specified**|Consente di usare la soglia specificata in **FDStrengthThreshold**. Il livello di attendibilità della dipendenza funzionale viene segnalato solo se è maggiore della soglia.|  
|**Exact**|Non specifica alcuna soglia. Il livello di attendibilità della dipendenza funzionale viene segnalato solo se la dipendenza funzionale tra le colonne selezionate è esatta.|  
  
 **FDStrengthThreshold**  
 Specifica la soglia (utilizzando un valore compreso tra 0 e 1) al di sopra del quale deve essere segnalato il livello di attendibilità della dipendenza funzionale. Il valore predefinito di questa proprietà è 0.95. Questa opzione è attivata solo quando si seleziona **Specified** come **ThresholdSetting**.  
  
 **MaxNumberOfViolations**  
 Specifica il numero massimo di violazioni della dipendenza funzionale da segnalare nell'output. Il valore predefinito di questa proprietà è 100. Questa opzione è disabilitata quando si seleziona **Exact** come **ThresholdSetting**.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor attività Profiling dati &#40;pagina Generale&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Form profilo rapido singola tabella &#40;Attività Profiling dati&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
