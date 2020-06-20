---
title: Opzioni di Richiesta profilo Distribuzione valori di colonna (Attività Profiling dati) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c1e5f5de-04f5-4d00-a9f0-55817186bdf9
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a18cc68954ba9427169458fc4f972f9ee878d822
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84919532"
---
# <a name="column-value-distribution-profile-request-options-data-profiling-task"></a>Opzioni di Richiesta profilo Distribuzione valori di colonna (Attività Profiling dati)
  Usare il riquadro **Proprietà richiesta** della pagina **Richieste profilo** per impostare le opzioni della **Richiesta profilo Distribuzione valori di colonna** selezionata nel riquadro delle richieste. Il profilo Distribuzione valori di colonna segnala tutti i valori distinct nella colonna selezionata e la percentuale di righe della tabella rappresentata da ogni valore. Può inoltre segnalare i valori che rappresentano più percentuali specificate di righe nella tabella. Il profilo consente infine di identificare eventuali problemi nei dati, ad esempio un numero non corretto di valori distinct in una colonna. Si analizza, ad esempio, una colonna contenente gli stati degli Stati Uniti e si individuano più di 50 valori distinct.  
  
> [!NOTE]  
>  Le opzioni descritte in questo argomento vengono visualizzate nella pagina **Richieste profilo** in **Editor attività Profiling dati**. Per altre informazioni su questa pagina dell'editor, vedere [Editor attività Profiling dati &#40;pagina Richieste profilo&#41;](data-profiling-task-editor-profile-requests-page.md).  
  
 Per altre informazioni su come usare l'attività Profiling dati, vedere [Impostazione dell'attività Profiling dati](data-profiling-task.md). Per altre informazioni sull'uso del Visualizzatore profilo dati per analizzare l'output dell'attività Profiling dati, vedere [Visualizzatore profilo dati](data-profile-viewer.md).  
  
## <a name="request-properties-options"></a>Opzioni del riquadro Proprietà richiesta  
 Nel riquadro **Proprietà richiesta**per **Richiesta profilo Distribuzione valori di colonna** vengono visualizzati i gruppi di opzioni seguenti:  
  
-   **Dati**che include le opzioni **TableOrView** e **Column**  
  
-   **Generale**  
  
-   **Opzioni**  
  
### <a name="data-options"></a>Opzioni dati  
 **ConnectionManager**  
 Consente di selezionare la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] esistente che usa il provider di dati .NET per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) ai fini della connessione al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente la tabella o la vista di cui eseguire il profiling.  
  
 **TableOrView**  
 Consente di selezionare la tabella o la vista esistente che contiene la colonna da analizzare.  
  
 Per ulteriori informazioni, vedere la sezione "Opzioni TableorView" in questo argomento.  
  
 **Colonna**  
 Consente di selezionare la colonna esistente da analizzare. Selezionare **(\*)** per analizzare tutte le colonne.  
  
 Per ulteriori informazioni, vedere la sezione "Opzioni Column" in questo argomento.  
  
#### <a name="tableorview-options"></a>Opzioni TableOrView  
 **Schema**  
 Specifica lo schema a cui appartiene la tabella selezionata. Questa opzione è di sola lettura.  
  
 **Tabella**  
 Visualizza il nome della tabella selezionata. Questa opzione è di sola lettura.  
  
#### <a name="column-options"></a>Opzioni relative alle colonne  
 **IsWildCard**  
 Specifica se è stato selezionato il carattere jolly **(\*)** . Questa opzione è impostata su **True** se è stato selezionato **(\*)** per profilare tutte le colonne. È impostata su **False** se è stata selezionata una singola colonna da analizzare. Questa opzione è di sola lettura.  
  
 **ColumnName**  
 Visualizza il nome della colonna selezionata. È vuota se è stato selezionato **(\*)** per profilare tutte le colonne. Questa opzione è di sola lettura.  
  
 **StringCompareOptions**  
 Consente di selezionare le opzioni per il confronto di valori stringa. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente. Il valore predefinito di questa opzione è **Default**.  
  
> [!NOTE]  
>  Se si usa il carattere jolly **(\*)** per **ColumnName**, la proprietà **CompareOptions** è di sola lettura ed è impostata su **Default**.  
  
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
 **ValueDistributionOption**  
 Consente di specificare se calcolare la distribuzione per tutti i valori di colonna. Il valore predefinito di questa opzione è **FrequentValues**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**AllValues**|La distribuzione viene calcolata per tutti i valori di colonna.|  
|**FrequentValues**|La distribuzione viene calcolata solo per i valori la cui frequenza supera il valore minimo specificato in **FrequentValueThreshold**. Valori che non soddisfano **FrequentValueThreshold** sono esclusi dal report di output.|  
  
 **FrequentValueThreshold**  
 Specifica la soglia (utilizzando un valore compreso tra 0 e 1) al di sopra della quale deve essere segnalato il valore di colonna. Questa opzione è disattivata quando si seleziona **AllValues** come **ValueDistributionOption**. Il valore predefinito di questa opzione è 0,001.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor attività Profiling dati &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)   
 [Form profilo rapido singola tabella &#40;Attività Profiling dati&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  
