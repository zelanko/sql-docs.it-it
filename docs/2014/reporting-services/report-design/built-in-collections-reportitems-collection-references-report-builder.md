---
title: Riferimenti alla raccolta ReportItems (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: edc0c75f-0530-4e6d-85aa-3385301bfd00
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 684ee8c4738b2cc46cb847820a2408365c1a5cd1
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56042832"
---
# <a name="reportitems-collection-references-report-builder-and-ssrs"></a>Riferimenti alla raccolta ReportItems (Generatore report e SSRS)
  La raccolta predefinita `ReportItems` è il set di caselle di testo di elementi del report, ad esempio righe di un'area dati o caselle di testo nell'area di progettazione del report. La raccolta `ReportItems` include caselle di testo che si trovano nell'ambito corrente di un'intestazione di pagina, un piè di pagina o il corpo di un report. Questa raccolta viene determinata in fase di esecuzione dal componente Elaborazione report e dal renderer di report. L'ambito corrente cambia quando il componente Elaborazione report combina in successione i dati del report e gli elementi di layout dei relativi elementi mentre l'utente visualizza le pagine di un report. È possibile utilizzare la raccolta predefinita `ReportItems` per produrre intestazioni di pagina in formato dizionario in cui vengono visualizzati il primo e l'ultimo elemento in ogni pagina.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-reportitems-value-property"></a>Utilizzo della proprietà Valute di ReportItems  
 Gli elementi all'interno di `ReportItems` raccolta hanno una sola proprietà: Valore. È possibile utilizzare il valore per un elemento di `ReportItems` per visualizzare o calcolare i dati di un altro campo del report. Per accedere al valore della casella di testo corrente, è possibile usare la proprietà globale predefinita Me.Value di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] o semplicemente Value. Nelle funzioni per i report come First e nelle funzioni di aggregazione utilizzare la sintassi completa.  
  
 Ad esempio:  
  
-   Questa espressione, se inserita in una casella di testo, visualizza il valore di una casella di testo `ReportItem` denominata `Textbox1`:  
  
     `=ReportItems!Textbox1.Value`  
  
-   Questa espressione, inserita un `ReportItem` proprietà Color, casella di testo Visualizza il testo in nero quando il valore è > 0; in caso contrario, il valore viene visualizzato in rosso:  
  
     `=IIF(Me.Value > 0,"Black","Red")`  
  
-   Questa espressione, se inserita in una casella di testo nell'intestazione o nel piè di pagina, visualizza il primo valore per ogni pagina del report visualizzabile, per una casella di testo denominata `LastName`:  
  
     `=First(ReportItems("LastName").Value)`  
  
## <a name="dictionary-style-page-header-expressions"></a>Espressioni per intestazioni di pagina in formato dizionario  
 È possibile creare un'intestazione di pagina in modo da visualizzare il primo e l'ultimo cliente nella pagina. Poiché una casella di testo nell'intestazione di pagina può fare riferimento alla raccolta predefinita `ReportItems` una sola volta in un'espressione, è necessario aggiungere due caselle di testo all'intestazione di pagina: una per il nome del primo cliente (`=First(ReportItems!textboxLastName.Value`) e l'altra per il nome dell'ultimo cliente (`=Last(ReportItems!textboxLastName.Value`).  
  
 In una sezione di intestazione o piè di pagina sono disponibili solo le caselle di testo della pagina corrente come membri della raccolta `ReportItems`. Ad esempio, se `ReportItems!textboxLastName.Value` fa riferimento a una casella di testo riportata solo nella prima pagina di un'area dati a più pagine, viene visualizzato un valore per la prima pagina, mentre per tutte le altre pagine viene visualizzato **#Errore** a indicare che l'espressione non può essere valutata come scritta.  
  
## <a name="scope-for-the-reportitems-collection"></a>Ambito per la raccolta ReportItems  
 Quando il report viene elaborato, ogni casella di testo nel corpo del report o in un'area dati viene valutata nel contesto del relativo set di dati, area dati e associazioni di gruppo. L'ambito per un riferimento alla raccolta `ReportItems` corrisponde all'ambito corrente o a qualsiasi punto superiore.  
  
 Ad esempio, una casella di testo in una riga appartenente a un gruppo padre non deve contenere un'espressione che fa riferimento al nome di una casella di testo in una riga di un gruppo figlio. Tale espressione non restituisce un valore nel report, perché la casella di testo nella riga figlio si trova al di fuori dell'ambito. Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](built-in-collections-in-expressions-report-builder.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
