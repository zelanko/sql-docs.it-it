---
title: Librerie di classi dell'elemento del report personalizzato | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items, RDL
- RDL [Reporting Services], custom report items
ms.assetid: f18c5d8f-1d6b-4f0b-8657-c14896c2ce0d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b7fc20f857f42c854fcf01947c39ea88206bb5b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63264885"
---
# <a name="custom-report-item-class-libraries"></a>Librerie di classi dell'elemento del report personalizzato
  Gli elementi del report personalizzati utilizzano le classi dello spazio dei nomi `Microsoft.ReportDesigner`. Le classi utilizzate per implementare un elemento del report personalizzato possono essere suddivise in due categorie principali: le classi univoche progettate per supportare l'infrastruttura dell'elemento del report personalizzato e le classi wrapper gestite che incapsulano la funzionalità degli elementi RDL (Report Definition Language) rilevanti. Per un esempio di codice sull'uso di queste classi, vedere [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (Esempi del prodotto SQL Server Reporting Services).  
  
## <a name="custom-report-item-infrastructure-classes"></a>Classi di infrastruttura dell'elemento del report personalizzato  
 Le classi riportate di seguito vengono utilizzate per implementare un elemento del report personalizzato.  
  
> [!NOTE]  
>  Nelle tabelle seguenti non vengono forniti elenchi completi, ma solo le proprietà e i metodi utilizzati più di frequente per ciascuna classe.  
  
### <a name="microsoftreportdesignercustomreportitemdesigner"></a>Microsoft.ReportDesigner.CustomReportItemDesigner  
 È la classe principale dell'elemento del report personalizzato. La classe principale dell'implementazione dell'elemento del report personalizzato deve ereditare da questa classe.  
  
#### <a name="public-properties"></a>Proprietà pubbliche  
  
|||  
|-|-|  
|`Name`|Nome dell'elemento del report personalizzato.|  
|`Type`|Tipo di elemento del report personalizzato.|  
|`CustomData`|Oggetto <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> che incapsula le proprietà dei dati dell'elemento del report personalizzato specificate in fase di progettazione.|  
|`CustomProperties`|Raccolta di proprietà personalizzate per l'elemento del report personalizzato.|  
|`Height`|Altezza del controllo dell'elemento del report personalizzato.|  
|`Width`|Larghezza del controllo dell'elemento del report personalizzato.|  
|`Report`|Contenitore per le proprietà a livello di report, ad esempio l'elenco dei set di dati nel report.|  
|`AltReportItem`|Oggetto elemento del report alternativo, da utilizzare se il controllo di runtime di un elemento del report personalizzato non è supportato.|  
|`Style`|Proprietà di stile per l'elemento del report personalizzato.|  
|`Adornment`|Finestra dell'area di controllo utilizzata per la modifica interattiva del controllo.|  
|`Site`|`ISite` del componente.|  
|`DesignerVerbCollection`|Matrice di verbi personalizzati per il menu di scelta rapida del controllo.|  
  
#### <a name="public-methods"></a>Metodi pubblici  
  
|||  
|-|-|  
|`BeginEdit`|Attiva la modifica interattiva per il controllo.|  
|`DoDefaultAction`|Viene chiamato quando si fa doppio clic o si preme Invio sul controllo.|  
|`EndEdit`|Disattiva la modifica interattiva per il controllo.|  
|`GetService`|Restituisce un oggetto che rappresenta un servizio.|  
|`InitializeNewComponent`|Viene chiamato quando si crea un nuovo elemento del report personalizzato.|  
|`Invalidate`|Ridisegna l'intera superficie del controllo.|  
|`OnDragEnter`<br /><br /> `OnDragDrop`|Viene chiamato quando si trascina un oggetto sul controllo.|  
|`OnPaint`|Viene chiamato in risposta all'evento `Paint`.|  
  
### <a name="microsoftreportdesignercustomreportitemattribute"></a>Microsoft.ReportDesigner.CustomReportItemAttribute  
 Attributo utilizzato per identificare il tipo di elemento del report personalizzato. Il nome deve corrispondere al valore della <`Name`> attributo del `ReportItem` elemento nel file di configurazione di progettazione Report.  
  
#### <a name="public-methods"></a>Metodi pubblici  
  
|||  
|-|-|  
|`CustomReportItemAttribute`|Crea l'oggetto CustomReportItemAttribute.|  
  
### <a name="microsoftreportdesignerlocalizednameattribute"></a>Microsoft.ReportDesigner.LocalizedNameAttribute  
 Attributo utilizzato per specificare il nome visualizzato da utilizzare per la finestra di progettazione dell'elemento del report personalizzato.  
  
#### <a name="public-methods"></a>Metodi pubblici  
  
|||  
|-|-|  
|`LocalizedNameAttribute`|Crea l'oggetto LocalizedNameAttribute.|  
  
### <a name="microsoftreportdesigneradornment"></a>Microsoft.ReportDesigner.Adornment  
 La classe `Adornment` viene utilizzata dal componente dell'elemento del report personalizzato per la fase di progettazione per fornire aree esterne al rettangolo principale dell'area di progettazione. Tali aree possono gestire eventi dell'interfaccia utente, quali clic del mouse e operazioni di trascinamento della selezione.  
  
#### <a name="public-methods"></a>Metodi pubblici  
  
|||  
|-|-|  
|`OnShow`|Viene chiamato quando viene attivato `Adornment`.|  
|`OnHide`|Viene chiamato quando viene disattivato `Adornment`.|  
|`Paint`|Viene chiamato in risposta all'evento `Paint`.|  
|`OnDragEnter`<br /><br /> `OnDragOver`<br /><br /> `OnDragLeave`<br /><br /> `OnDragDrop`|Viene chiamato quando un oggetto viene trascinato in `Adornment`.|  
  
### <a name="microsoftreportdesigneradornerservice"></a>Microsoft.ReportDesigner.AdornerService  
 Questa classe viene utilizzata per fornire una raccolta di servizi visualizzati utilizzati dall'elemento del report personalizzato per supportare gli oggetti `Adornment` per il componente della fase di progettazione dell'elemento del report personalizzato.  
  
#### <a name="public-properties"></a>Proprietà pubbliche  
  
|||  
|-|-|  
|`AdornerWindowBounds`|Limiti della finestra Adorner.|  
|`AdornerWindowRegion`|Area della finestra Adorner.|  
|`AdornerWindowGraphics`|Contesto grafico per la finestra Adorner.|  
  
#### <a name="public-methods"></a>Metodi pubblici  
  
|||  
|-|-|  
|`ComponentRectInDesignerFrame`|Restituisce i limiti del componente convertito nelle coordinate della cornice della finestra di progettazione.|  
|`InvalidateAdorner`|Invalida la finestra Adorner.|  
|`PointToAdorner`|Restituisce un punto nelle coordinate dello schermo convertito nelle coordinate della finestra Adorner.|  
  
### <a name="microsoftreportdesignerexpressioneditor"></a>Microsoft.ReportDesigner.ExpressionEditor  
 Questa classe può essere utilizzata da un controllo della fase di progettazione dell'elemento del report personalizzato per richiamare l'Editor espressioni.  
  
#### <a name="public-methods"></a>Metodi pubblici  
  
|||  
|-|-|  
|`EditValue`|Richiama l'Editor espressioni, inizializzato con il valore dell'oggetto specificato.|  
  
### <a name="microsoftreportdesignerifieldsdataobject"></a>Microsoft.ReportDesigner.IFieldsDataObject  
 Questa classe è una raccolta di campi di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e viene utilizzata per supportare eventi di trascinamento della selezione nell'ambiente di progettazione. Eredita da `IReportItemDataObject`.  
  
#### <a name="public-properties"></a>Proprietà pubbliche  
  
|||  
|-|-|  
|`DataSetName`|Nome del set di dati contenente i campi da eliminare.|  
|`Fields`|Raccolta di campi (`Microsoft.ReportDesigner.Field`) da eliminare.|  
  
## <a name="see-also"></a>Vedere anche  
 [Report Definition Language &#40;SSRS&#41;](../reports/report-definition-language-ssrs.md)   
 [Creazione di un componente runtime dell'elemento del report personalizzato](creating-a-custom-report-item-run-time-component.md)   
 [Creazione di un componente dell'elemento del report personalizzato per la fase di progettazione](creating-a-custom-report-item-design-time-component.md)  
  
  
