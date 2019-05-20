---
title: Raccolte predefinite nelle espressioni (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 78d5e3b8-9320-4e4b-a025-e2de3cf7afa7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 684f8dd2b74597b96018449492abe3786e0acba0
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65581782"
---
# <a name="built-in-collections-in-expressions-report-builder"></a>Raccolte predefinite nelle espressioni (Generatore report e SSRS)
  Nell'espressione di un report è possibile includere riferimenti alle raccolte predefinite seguenti: ReportItems, Parameters, Fields, DataSets, DataSources, Variables e a campi predefiniti per informazioni generali quali il nome del report. Nella finestra di dialogo **Espressione** non vengono visualizzate tutte le raccolte. Le raccolte DataSets e DataSources sono disponibili solo in fase di progettazione per i report pubblicati in un server di report. ReportItems è una raccolta di caselle di testo in un'area del report, ad esempio le caselle di testo visualizzate in una pagina o in un'intestazione.  
  
 Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Collections"></a> Informazioni sulle raccolte predefinite  
 Nella tabella seguente sono elencate le raccolte predefinite disponibili quando si scrive un'espressione. Ogni riga include il nome a livello di programmazione della raccolta, con distinzione tra maiuscole e minuscole, l'indicazione se è possibile utilizzare la finestra di dialogo Espressione per aggiungere un riferimento alla raccolta in modo interattivo, un esempio e una descrizione in cui è specificato quando vengono inizializzati i valori della raccolta e sono quindi disponibili per l'uso.  
  
|Raccolta predefinita|Categoria nella finestra di dialogo Espressione|Esempio|Descrizione|  
|--------------------------|-------------------------------------------|-------------|-----------------|  
|**Elementi globali**|Campi predefiniti|`=Globals.ReportName`<br /><br /> `- or -`<br /><br /> `=Globals.PageNumber`|Rappresenta le variabili globali utili per i report, quali il nome del report o il numero di pagina. Sempre disponibile.<br /><br /> Per altre informazioni, vedere [Riferimenti alle raccolte predefinite Globals e Users &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).|  
|**Utente**|Campi predefiniti|`=User.UserID`<br /><br /> - oppure -<br /><br /> `=User.Language`|Rappresenta una raccolta di dati relativi all'utente che esegue il report, ad esempio l'impostazione della lingua o l'ID utente. Sempre disponibile.<br /><br /> Per altre informazioni, vedere [Riferimenti alle raccolte predefinite Globals e Users &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).|  
|**Parametri**|Parametri|`=Parameters("ReportMonth").Value`<br /><br /> - oppure -<br /><br /> `=Parameters!ReportYear.Value`|Rappresenta la raccolta dei parametri del report, che possono essere a valore singolo o multivalore. Non disponibile prima del completamento dell'inizializzazione dell'elaborazione. Per altre informazioni, vedere [Riferimenti alla raccolta dei parametri &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md).|  
|**Campi(** *\<Set di dati>* **)**|Campi|`=Fields!Sales.Value`|Rappresenta la raccolta di campi del set di dati disponibili per il report. Disponibile dopo il recupero dei dati da un'origine dei dati in un set di dati. Per altre informazioni, vedere [Riferimenti alla raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md).|  
|**DataSets**|Non visualizzata|`=DataSets("TopEmployees").CommandText`|Rappresenta la raccolta di set di dati a cui si fa riferimento nel corpo della definizione del report. Non include origini dei dati utilizzate solo nelle intestazioni pagina o nei piè di pagina. Non disponibile nell'anteprima locale. Per altre informazioni, vedere [Riferimenti a raccolte DataSources e DataSets &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md).|  
|**DataSources**|Non visualizzata|`=DataSources("AdventureWorks2012").Type`|Rappresenta la raccolta di origini dei dati a cui viene fatto riferimento nel corpo di un report. Non include origini dei dati utilizzate solo nelle intestazioni pagina o nei piè di pagina. Non disponibile nell'anteprima locale. Per altre informazioni, vedere [Riferimenti a raccolte DataSources e DataSets &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md).|  
|**Variabili**|`Variables`|`=Variables!CustomTimeStamp.Value`|Rappresenta la raccolta di variabili del report e variabili di gruppo. Per altre informazioni, vedere [Riferimenti a raccolte di variabili di report e di gruppo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md).|  
|**ReportItems**|Non visualizzata|`=ReportItems("Textbox1").Value`|Rappresenta la raccolta di caselle di testo per un elemento del report. Questa raccolta può essere utilizzata per riepilogare gli elementi nella pagina da includere in un'intestazione o in un piè di pagina. Per altre informazioni, vedere [Riferimenti alla raccolta ReportItems &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-reportitems-collection-references-report-builder.md).|  
  
##  <a name="Syntax"></a> Utilizzo della sintassi delle raccolte in un'espressione  
 Per fare riferimento a una raccolta in un'espressione, utilizzare la sintassi standard di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] per un elemento di una raccolta. Nella tabella seguente sono illustrati alcuni esempi di sintassi di raccolta.  
  
|Sintassi|Esempio|  
|------------|-------------|  
|*Collection!ObjectName.Property*|`=Fields!Sales.Value`|  
|*Collection!ObjectName("Property")*|`=Fields!Sales("Value")`|  
|*Collection("ObjectName").Property*|`=Fields("Sales").Value`|  
|*Collection("Member")*|`=User("Language")`|  
|*Collection.Member*|`=User.Language`|  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere un'espressione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
