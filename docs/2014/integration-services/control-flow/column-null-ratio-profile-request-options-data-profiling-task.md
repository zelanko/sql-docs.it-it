---
title: Opzioni di Richiesta profilo Rapporto di valori Null nella colonna (Attività Profiling dati) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 157ef8e4-fd23-4f81-8194-eebf74e9fd86
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 72b426c504532f9c112eaaa1222b0349f3e5d814
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374589"
---
# <a name="column-null-ratio-profile-request-options-data-profiling-task"></a>Opzioni di Richiesta profilo Rapporto di valori Null nella colonna (Attività Profiling dati)
  Utilizzare il riquadro **Proprietà richiesta** della pagina **Richieste profilo** per impostare le opzioni per la richiesta **Richiesta profilo Rapporto di valori Null nella colonna** selezionata nel riquadro delle richieste. Il profilo Rapporto di valori Null nella colonna segnala la percentuale di valori Null nella colonna selezionata e consente di identificare eventuali problemi nei dati, ad esempio un rapporto inaspettatamente elevato di valori Null in una colonna. Un profilo Rapporto di valori Null nella colonna può analizzare, ad esempio, una colonna contenente CAP e individuare una percentuale eccessivamente elevata di CAP mancanti.  
  
> [!NOTE]  
>  Le opzioni descritte in questo argomento vengono visualizzate nella pagina **Richieste profilo** in **Editor attività Profiling dati**. Per altre informazioni su questa pagina dell'editor, vedere [Editor attività Profiling dati &#40;pagina Richieste profilo&#41;](data-profiling-task-editor-profile-requests-page.md).  
  
 Per altre informazioni su come usare l'attività Profiling dati, vedere [Impostazione dell'attività Profiling dati](data-profiling-task.md). Per altre informazioni sull'uso del Visualizzatore profilo dati per analizzare l'output dell'attività Profiling dati, vedere [Visualizzatore profilo dati](data-profile-viewer.md).  
  
## <a name="request-properties-options"></a>Opzioni del riquadro Proprietà richiesta  
 Nel riquadro **Proprietà richiesta**per **Richiesta profilo Rapporto di valori Null nella colonna** vengono visualizzati i gruppi di opzioni seguenti:  
  
-   **Dati**che include le opzioni **TableOrView** e **Column**  
  
-   **Generale**  
  
### <a name="data-options"></a>Opzioni dati  
 **ConnectionManager**  
 Consente di selezionare la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] esistente che usa il provider di dati .NET per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) per la connessione al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente la tabella o la vista di cui eseguire il profiling.  
  
 **TableOrView**  
 Consente di selezionare la tabella o la vista esistente che contiene la colonna da analizzare.  
  
 Per ulteriori informazioni, vedere la sezione "Opzioni TableorView" in questo argomento.  
  
 **Column**  
 Consente di selezionare la colonna esistente da analizzare. Selezionare **(\*)** per analizzare tutte le colonne.  
  
 Per ulteriori informazioni, vedere la sezione "Opzioni Column" in questo argomento.  
  
#### <a name="tableorview-options"></a>Opzioni TableOrView  
 **Schema**  
 Specifica lo schema a cui appartiene la tabella selezionata. Questa opzione è di sola lettura.  
  
 **Tabella**  
 Visualizza il nome della tabella selezionata. Questa opzione è di sola lettura.  
  
#### <a name="column-options"></a>Opzioni relative alle colonne  
 **IsWildCard**  
 Specifica se è stato selezionato il carattere jolly **(\*)**. Questa opzione è impostata su **True** se è stato selezionato **(\*)** per profilare tutte le colonne. È impostata su **False** se è stata selezionata una singola colonna da analizzare. Questa opzione è di sola lettura.  
  
 **ColumnName**  
 Visualizza il nome della colonna selezionata. È vuota se è stato selezionato **(\*)** per profilare tutte le colonne. Questa opzione è di sola lettura.  
  
 **StringCompareOptions**  
 Questa opzione non si applica al profilo Rapporto di valori Null nella colonna.  
  
### <a name="general-options"></a>Opzioni generali  
 **RequestID**  
 Nome descrittivo per identificare la richiesta di profilo. Non è in genere necessario modificare il valore generato automaticamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor attività Profiling dati &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)   
 [Form profilo rapido singola tabella &#40;Attività Profiling dati&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  
