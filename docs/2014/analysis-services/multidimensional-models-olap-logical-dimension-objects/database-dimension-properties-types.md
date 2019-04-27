---
title: Tipi di dimensione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- time dimensions [Analysis Services]
- quantitative dimensions [Analysis Services]
- BillOfMaterials dimension [Analysis Services]
- geography dimensions
- utility dimensions [Analysis Services]
- channel dimensions
- dimensions [Analysis Services], types
- products dimensions [Analysis Services]
- account dimensions [Analysis Services]
- organization dimensions
- currency dimensions [Analysis Services]
- rates dimensions
- promotion dimensions
- scenario dimensions [Analysis Services]
- customers dimensions [Analysis Services]
- Type property
ms.assetid: bd3195da-e762-4c98-b643-34c76e842343
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cbe1c8932c082ce537cd5dc3f2b12d98c05c3811
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728557"
---
# <a name="dimension-types"></a>Tipi di dimensioni
  L'impostazione della proprietà `Type` offre informazioni sui contenuti di una dimensione alle applicazioni server e client. In alcuni casi, l'impostazione `Type` offre informazioni solo alle applicazioni client ed è facoltativa. In altri casi, ad esempio le dimensioni `Accounts` o `Time`, le impostazioni della proprietà `Type` per la dimensione e i relativi attributi determinano comportamenti specifici basati sul server e possono essere necessarie per implementare determinati comportamenti nel cubo. La proprietà `Type` di una dimensione, ad esempio, può essere impostata su `Accounts` per indicare alle applicazioni client che la dimensione standard contiene attributi Conto. Per altre informazioni sull'ora, l'account e dimensioni di tipo valuta, vedere [creare una dimensione di tipo data](../multidimensional-models/database-dimensions-create-a-date-type-dimension.md), [creare un conto finanziario della dimensione di tipo padre-figlio](../multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md), e [creare una valuta tipo di dimensione](../multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 L'impostazione predefinita per il tipo di dimensione è `Regular`, che non indica alcun tipo specifico di contenuto della dimensione. Questa è l'impostazione predefinita per tutte le dimensioni al momento della creazione, a meno che in fase di definizione della dimensione tramite la Creazione guidata dimensione non si specifichi `Time`. È inoltre consigliabile lasciare `Regular` come tipo di dimensione impostato, se nella Creazione guidata dimensione non è elencato alcun tipo di dimensione appropriato.  
  
## <a name="available-dimension-types"></a>Tipi di dimensioni disponibili  
 Nella tabella seguente vengono descritti i tipi di dimensione disponibili nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Tipo dimensione|Descrizione|  
|--------------------|-----------------|  
|Regular|Dimensione il cui tipo non è stato impostato in base a un valore speciale.|  
|Time|Dimensione i cui attributi rappresentano periodi di tempo, ad esempio anni, semestri, trimestri, mesi e giorni.|  
|Organization|Dimensione i cui attributi rappresentano informazioni sull'organizzazione, ad esempio dipendenti o filiali.|  
|Geography|Dimensione i cui attributi rappresentano informazioni geografiche, ad esempio città o CAP.|  
|BillOfMaterials|Dimensione i cui attributi rappresentano informazioni relative alle scorte o alla produzione, ad esempio elenchi di parti di prodotti.|  
|Account|Dimensione i cui attributi rappresentano un grafico dei conti per la generazione di report finanziari.|  
|Customers|Dimensione i cui attributi rappresentano informazioni sui clienti o sui contatti.|  
|Products|Dimensione i cui attributi rappresentano informazioni sui prodotti.|  
|Scenario|Dimensione i cui attributi rappresentano informazioni di pianificazione o di analisi strategica.|  
|Quantitative|Dimensione i cui attributi rappresentano informazioni sulle quantità.|  
|Utilità|Dimensione i cui attributi rappresentano informazioni di vario tipo.|  
|Currency|Questo tipo di dimensione contiene dati e metadati relativi alla valuta.|  
|Rates|Dimensione i cui attributi rappresentano informazioni sui tassi valutari.|  
|Channel|Dimensione i cui attributi rappresentano informazioni sul canale.|  
|Promotion|Dimensione i cui attributi rappresentano informazioni sulle promozioni marketing.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una dimensione utilizzando una tabella esistente](../multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [Dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
