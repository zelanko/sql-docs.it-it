---
title: Specificare il tipo di dimensione (Creazione guidata dimensione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.bidimensionproperties.f1
ms.assetid: 3215282a-532d-4ff2-b721-286f088967fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6de1b056942673d358cec4768c6854a6966d139e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068368"
---
# <a name="specify-dimension-type-dimension-wizard"></a>Impostazione tipo di dimensione (Creazione guidata dimensione)
  Usare la pagina **Impostazione tipo di dimensione** per definire il tipo di dimensione e aggiungere alla dimensione i tipi di attributo speciali associati al tipo di dimensione selezionato.  
  
> [!NOTE]  
>  Questa pagina viene visualizzata solo se è stata selezionata l'opzione **Dimensione standard** nella pagina **Selezione tipo di dimensione** .  
  
## <a name="options"></a>Opzioni  
 **Tipo di dimensione**  
 Consente di selezionare il tipo di dimensione. Nella tabella seguente vengono descritti i tipi di dimensione disponibili.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Accounts**|Le dimensioni di tipo Conti contengono dati e metadati che rappresentano un elenco di conti.<br /><br /> Per altre informazioni sulle dimensioni di tipo Conti, vedere [Creare un conto finanziario della dimensione di tipo padre-figlio](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).|  
|**BillOfMaterials**|Le dimensioni di tipo Distinta base sono dimensioni regolari nelle quali i dati e i metadati rappresentano informazioni di inventario o di produzione, ad esempio elenchi di parti per i prodotti.<br /><br /> Per altre informazioni sulle dimensioni regolari, vedere [Tipi di dimensioni](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Channel**|Le dimensioni di tipo Channel sono dimensioni regolari nelle quali i dati e i metadati rappresentano informazioni di canale.<br /><br /> Per altre informazioni sulle dimensioni regolari, vedere [Tipi di dimensioni](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Currency**|Le dimensioni di tipo Valuta contengono dati e metadati che rappresentano informazioni di valuta.<br /><br /> Per altre informazioni sulle dimensioni di tipo Valuta, vedere [Creare una dimensione di tipo Valuta](multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).|  
|**Customers**|Le dimensioni di tipo Customer sono dimensioni regolari nelle quali i dati e i metadati rappresentano informazioni di cliente o di contatto.<br /><br /> Per altre informazioni sulle dimensioni regolari, vedere [Tipi di dimensioni](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Geography**|Le dimensioni di tipo Geography sono dimensioni regolari nelle quali i dati e i metadati rappresentano informazioni geografiche, ad esempio città o CAP.<br /><br /> Per altre informazioni sulle dimensioni regolari, vedere [Tipi di dimensioni](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Organization**|Le dimensioni di tipo Organization sono dimensioni regolari nelle quali i dati e i metadati rappresentano informazioni sull'organizzazione, ad esempio dipendenti o filiali.<br /><br /> Per altre informazioni sulle dimensioni regolari, vedere [Tipi di dimensioni](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Prodotti**|Le dimensioni di tipo Product sono dimensioni regolari nelle quali i dati e i metadati rappresentano informazioni di prodotto.<br /><br /> Per altre informazioni sulle dimensioni regolari, vedere [Tipi di dimensioni](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Promotion**|Le dimensioni di tipo Promotion sono dimensioni regolari nelle quali i dati e i metadati rappresentano informazioni promozionali di marketing.<br /><br /> Per altre informazioni sulle dimensioni regolari, vedere [Tipi di dimensioni](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Quantitative**|Le dimensioni di tipo Quantitative sono dimensioni regolari nelle quali i dati e i metadati rappresentano informazioni quantitative.<br /><br /> Per altre informazioni sulle dimensioni regolari, vedere [Tipi di dimensioni](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Tariffe**|Le dimensioni di tipo Rate contengono dati e metadati che rappresentano informazioni di tassi di cambio e di conversione valuta.|  
|**Regular**|Le dimensioni regolari sono le dimensioni più comunemente usate in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].<br /><br /> Per altre informazioni sulle dimensioni regolari, vedere [Tipi di dimensioni](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Scenario**|Le dimensioni di tipo Scenario sono dimensioni regolari nelle quali i dati e i metadati rappresentano informazioni di pianificazione o di analisi strategica.<br /><br /> Per altre informazioni sulle dimensioni regolari, vedere [Tipi di dimensioni](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Time**|Le dimensioni temporali contengono dati e metadati basati sul tempo.<br /><br /> Per altre informazioni sulle dimensioni temporali, vedere [Creare una dimensione di tipo Date](multidimensional-models/database-dimensions-create-a-date-type-dimension.md).|  
|**Utilità**|Le dimensioni di tipo Utility sono dimensioni regolari nelle quali i dati e i metadati rappresentano informazioni che non corrispondono immediatamente a un altro tipo di dimensione.<br /><br /> Per altre informazioni sulle dimensioni regolari, vedere [Tipi di dimensioni](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
  
## <a name="dimension-attributes-options"></a>Opzioni degli attributi della dimensione  
  
> [!NOTE]  
>  Le opzioni descritte in questa sezione diventano disponibili solo se il **Tipo dimensione** selezionato è associato a tipi di attributo speciali. Non tutti i tipi di dimensione sono associati a tipi di attributo speciali.  
  
 **Include**  
 Selezionare la casella di controllo per includere il tipo di attributo nella dimensione.  
  
 **Tipo di attributo**  
 Consente di visualizzare il tipo di attributo associato al tipo di dimensione selezionato in **Tipo dimensione**. Per altre informazioni sui tipi di attributo, vedere [Elemento Type &#40;DimensionAttribute&#41; &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/type-element-dimensionattribute-assl).  
  
 **Attributo della dimensione**  
 Consente di selezionare l'attributo di dimensione al quale la Creazione guidata dimensione assegnerà il tipo di attributo speciale visualizzato in **Tipo attributo**.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida F1 di creazione guidata dimensione](dimension-wizard-f1-help.md)   
 [Dimensioni &#40;Analysis Services - dati multidimensionali&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensioni nei modelli multidimensionali](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
