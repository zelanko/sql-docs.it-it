---
title: Tipi di dimensione | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 663c26ac169c11e5ab2d9b90285419cf4145368c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025772"
---
# <a name="database-dimension-properties---types"></a>Proprietà delle dimensioni del database - Tipi
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Il **tipo** l'impostazione della proprietà fornisce informazioni sul contenuto di una dimensione alle applicazioni client e server. In alcuni casi, il **tipo** impostazione solo fornisce materiale sussidiario per le applicazioni client ed è facoltativa. In altri casi, ad esempio **account** o **ora** dimensioni, il **tipo** impostazioni delle proprietà per la dimensione e i relativi attributi determinano comportamenti specifici basati su server e potrebbe essere necessario per implementare determinati comportamenti nel cubo. Ad esempio, il **tipo** proprietà di una dimensione può essere impostata su **account** per indicare alle applicazioni client che la dimensione standard contiene attributi conto. Per altre informazioni sull'ora, l'account e dimensioni di tipo valuta, vedere [creare una dimensione di tipo data](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md), [creare un conto finanziario della dimensione di tipo padre-figlio](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md), e [creare una valuta tipo di dimensione](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 L'impostazione predefinita per il tipo di dimensione **regolari**, che non fa alcuna ipotesi sui contenuti della dimensione. Si tratta dell'impostazione predefinita per tutte le dimensioni quando si definisce inizialmente una dimensione a meno che non si specifica **ora** quando si definisce la dimensione mediante Creazione guidata dimensione. È inoltre consigliabile lasciare **regolari** come tipo di dimensione, se la creazione guidata dimensione non è elencato un tipo appropriato per il tipo di dimensione.  
  
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
 [Creare una dimensione utilizzando una tabella esistente](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [Dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
