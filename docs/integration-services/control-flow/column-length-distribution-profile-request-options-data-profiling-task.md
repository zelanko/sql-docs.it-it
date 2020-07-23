---
title: Opzioni di Richiesta profilo Distribuzione lunghezze di colonna (Attività Profiling dati) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 1a4de41f-f38d-40ea-ba1b-6c0ef67ea52a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0f3833327f518b935874b79747ef9cd6b129143a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921427"
---
# <a name="column-length-distribution-profile-request-options-data-profiling-task"></a>Opzioni di Richiesta profilo Distribuzione lunghezze di colonna (Attività Profiling dati)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Usare il riquadro **Proprietà richiesta** della pagina **Richieste profilo** per impostare le opzioni della richiesta **Richiesta profilo Distribuzione lunghezze di colonna** selezionata nel riquadro delle richieste. Il profilo Distribuzione lunghezze di colonna segnala tutte le singole lunghezze dei valori stringa nella colonna selezionata e la percentuale di righe nella tabella rappresentata da ogni lunghezza. Questo profilo consente inoltre di identificare eventuali problemi nei dati, ad esempio valori non validi. Si analizza, ad esempio, una colonna di codici a due caratteri degli stati degli Stati Uniti e si individuano valori con lunghezza maggiore di due caratteri.  
  
> [!NOTE]  
>  Le opzioni descritte in questo argomento vengono visualizzate nella pagina **Richieste profilo** in **Editor attività Profiling dati**. Per altre informazioni su questa pagina dell'editor, vedere [Editor attività Profiling dati &#40;pagina Richieste profilo&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Per altre informazioni su come usare l'attività Profiling dati, vedere [Impostazione dell'attività Profiling dati](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Per altre informazioni sull'uso del Visualizzatore profilo dati per analizzare l'output dell'attività Profiling dati, vedere [Visualizzatore profilo dati](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="request-properties-options"></a>Opzioni del riquadro Proprietà richiesta  
 Nel riquadro **Proprietà richiesta**per **Richiesta profilo Distribuzione lunghezze di colonna** vengono visualizzati i gruppi di opzioni seguenti:  
  
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
 Questa opzione non si applica al profilo Distribuzione lunghezze di colonna.  
  
### <a name="general-options"></a>Opzioni generali  
 **RequestID**  
 Nome descrittivo per identificare la richiesta di profilo. Non è in genere necessario modificare il valore generato automaticamente.  
  
### <a name="options"></a>Opzioni  
 **IgnoreLeadingSpaces**  
 Indica se ignorare gli spazi iniziali quando il profilo confronta i valori stringa. Il valore predefinito di questa opzione è **False**.  
  
 **IgnoreTrailingSpaces**  
 Indica se ignorare gli spazi finali quando il profilo confronta i valori stringa. Il valore predefinito di questa opzione è **True**.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor attività Profiling dati &#40;pagina Generale&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Form profilo rapido singola tabella &#40;Attività Profiling dati&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
