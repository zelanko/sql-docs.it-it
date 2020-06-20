---
title: Proprietà del flusso di dati che possono essere impostate tramite espressioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, property expressions
- Integration Services packages, property expressions
- packages [Integration Services], properties
- SSIS packages, property expressions
- property expressions [Integration Services]
ms.assetid: cd0e171a-08be-45d6-81dc-ed94f37698b8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3d23037bc09b735fc28e52eabb1852d1af303d15
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84916951"
---
# <a name="data-flow-properties-that-can-be-set-by-using-expressions"></a>Proprietà del flusso di dati che è possibile impostare tramite espressioni
  I valori di determinate proprietà di oggetti del flusso di dati possono essere specificati utilizzando espressioni di proprietà disponibili nel contenitore dell'attività Flusso di dati.  
  
 Per informazioni sull'utilizzo delle espressioni di proprietà, vedere [utilizzo delle espressioni di proprietà nei pacchetti](expressions/use-property-expressions-in-packages.md).  
  
 È possibile utilizzare espressioni di proprietà per personalizzare la configurazione di ogni istanza di pacchetto distribuita. È anche possibile usare espressioni di proprietà per specificare i vincoli in fase di esecuzione per un pacchetto tramite l'opzione **/set** con l'utilità del prompt dei comandi **dtexec** . Ad esempio, è possibile vincolare `MaximumThreads` utilizzato dalla trasformazione dell'ordinamento o `MaxMemoryUsage` delle trasformazioni del raggruppamento fuzzy e della ricerca fuzzy. Se non vincolate, queste trasformazioni possono memorizzare nella cache grandi quantità di dati.  
  
 Per specificare un'espressione di proprietà per una delle proprietà degli oggetti del flusso di dati elencate in questo argomento, visualizzare la finestra **Proprietà** per l'attività flusso di dati selezionando l'attività flusso di dati nell'area di progettazione **Flusso di controllo** o selezionando la scheda **Flusso di dati** della finestra di progettazione senza selezionare componenti o percorsi singoli. Selezionare la proprietà **Espressioni** e fare clic sui puntini di sospensione per visualizzare la finestra di dialogo **Editor espressioni di proprietà** . Visualizzare l'elenco a discesa **Proprietà** per selezionare una proprietà, quindi digitare un'espressione nella casella di testo **Espressione** o fare clic sui puntini di sospensione per visualizzare la finestra di dialogo **Generatore di espressioni** .  
  
 Nell'elenco **Proprietà** vengono visualizzate le proprietà disponibili per gli oggetti del flusso di dati già posizionati nell'area di progettazione **Flusso di dati** . Pertanto, non è possibile usare l'elenco **Proprietà** per visualizzare tutte le possibili proprietà degli oggetti del flusso di dati che supportano le espressioni di proprietà. Se, ad esempio, è stata posizionata un'origine ADO NET nell'area di progettazione, l'elenco delle **Proprietà** contiene una voce per la `[ADO NET Source].[SqlCommand]` Proprietà. Nell'elenco vengono anche visualizzate molte proprietà dell'attività Flusso di dati.  
  
## <a name="properties-of-data-flow-objects-that-support-property-expressions"></a>Proprietà degli oggetti del flusso di dati che supportano le espressioni Proprietà  
 È possibile specificare i valori delle proprietà del seguente elenco utilizzando le espressioni di proprietà.  
  
### <a name="data-flow-sources"></a>Origini del flussi di dati  
  
|Oggetto del flusso di dati|Proprietà|  
|----------------------|--------------|  
|Origine ADO NET|Proprietà TableOrViewName<br /><br /> Proprietà SqlCommand|  
|Origine XML|Proprietà XMLData<br /><br /> Proprietà XMLSchemaDefinition|  
  
### <a name="data-flow-transformations"></a>Trasformazioni del flusso di dati  
 Per altre informazioni su queste proprietà personalizzate, vedere [proprietà personalizzate della trasformazione](data-flow/transformations/transformation-custom-properties.md).  
  
|Oggetto del flusso di dati|Proprietà|  
|----------------------|--------------|  
|Suddivisione condizionale - trasformazione|Proprietà FriendlyExpression|  
|Trasformazione Colonna derivata|Proprietà FriendlyExpression|  
|Raggruppamento fuzzy - trasformazione|Proprietà MaxMemoryUsage|  
|Ricerca fuzzy - trasformazione|Proprietà MaxMemoryUsage|  
|Trasformazione Ricerca|Proprietà SqlCommand<br /><br /> Proprietà SqlCommandParam|  
|Comando OLE DB - trasformazione|Proprietà SqlCommand|  
|Campionamento percentuale - trasformazione|Proprietà SamplingValue|  
|Pivot - trasformazione|Proprietà PivotKeyValue|  
|Campionamento righe - trasformazione|Proprietà SamplingValue|  
|Ordinamento - trasformazione|Proprietà MaximumThreads|  
|UnPivot - trasformazione|Proprietà PivotKeyValue|  
  
### <a name="data-flow-destinations"></a>Destinazioni del flusso di dati  
  
|Oggetto del flusso di dati|Proprietà|  
|----------------------|--------------|  
|Destinazione ADO NET|Proprietà TableOrViewName<br /><br /> Proprietà BatchSize<br /><br /> Proprietà CommandTimeout|  
|file flat - destinazione|Proprietà dell'intestazione|  
|Destinazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact|Proprietà TableName|  
|Destinazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Proprietà BulkInsertTableName<br /><br /> Proprietà BulkInsertFirstRow<br /><br /> Proprietà BulkInsertLastRow<br /><br /> Proprietà BulkInsertOrder<br /><br /> Proprietà Timeout|  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Aggiunta o modifica di un'espressione di proprietà](expressions/add-or-change-a-property-expression.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Articolo tecnico relativo al [foglio d'aiuto per le espressioni SSIS](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet)sul sito Web pragmaticworks.com  
  
## <a name="see-also"></a>Vedere anche  
 [Usare espressioni di proprietà nei pacchetti](expressions/use-property-expressions-in-packages.md)   
 [Proprietà comuni](../../2014/integration-services/common-properties.md)   
 [Proprietà personalizzate della trasformazione](data-flow/transformations/transformation-custom-properties.md)   
 [Proprietà del percorso](../../2014/integration-services/path-properties.md)  
  
  
