---
title: Riferimenti alla raccolta dei parametri (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c4b47e15-0484-4c13-9182-898db825f01f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 137eb9b9cf7a5a64843e163ece3b4767dd8e1852
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581797"
---
# <a name="built-in-collections---parameters-collection-references-report-builder"></a>Raccolte predefinite- Riferimenti alla raccolta dei parametri (Generatore report)
  I parametri di un report sono una delle raccolte predefinite a cui è possibile fare riferimento da un'espressione. Includendo parametri in un'espressione, è possibile personalizzare i dati e l'aspetto dei report in base alle opzioni scelte da un utente. È possibile usare le espressioni per qualsiasi proprietà degli elementi del report o delle caselle di testo che includa l'opzione (*Fx*) o \<**Espressione**>. Le espressioni vengono anche utilizzate per controllare il contenuto e l'aspetto dei report in altri modi. Per altre informazioni, vedere [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md).  
  
 Quando si confrontano i valori dei parametri con i valori dei campi di set di dati in fase di esecuzione, i tipi di dati per i due elementi confrontati devono essere identici. I parametri dei report possono essere dei tipi seguenti: Boolean, DateTime, Integer, Float o Text, che rappresenta il tipo di dati stringa sottostante. Può essere necessario convertire il tipo di dati del valore del parametro in base al valore del set di dati. Per altre informazioni, vedere [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md).  
  
 Per includere un riferimento a un parametro in un'espressione, è necessario essere in grado di specificare la sintassi corretta per tale riferimento, che varia a seconda che il parametro sia a valore singolo o multivalore.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Single"></a> Utilizzo di un parametro a valore singolo in un'espressione  
 Nella tabella seguente sono riportati esempi della sintassi da utilizzare quando si include in un'espressione un riferimento a un parametro a valore singolo di un tipo di dati qualsiasi.  
  
|Esempio|Descrizione|  
|-------------|-----------------|  
|`=Parameters!` *\<NomeParametro>* `.IsMultiValue`|Restituisce **False**.<br /><br /> Verifica se un parametro è multivalore. Se è **True**, il parametro è multivalore ed è costituito da una raccolta di oggetti. Se è **False**, il parametro è a valore singolo ed è costituito da un solo oggetto.|  
|`=Parameters!` *\<NomeParametro>* `.Count`|Restituisce il valore intero 1. Per un parametro a valore singolo, il conteggio è sempre 1.|  
|`=Parameters!` *\<NomeParametro>* `.Label`|Restituisce l'etichetta del parametro, utilizzata di frequente come nome visualizzato in un elenco a discesa di valori disponibili.|  
|`=Parameters!` *\<NomeParametro>* `.Value`|Restituisce il valore del parametro. Se la proprietà Etichetta non è stata impostata, questo valore verrà visualizzato nell'elenco a discesa dei valori disponibili.|  
|`=CStr(Parameters!`  *\<NomeParametro>* `.Value)`|Restituisce il valore del parametro sotto forma di stringa.|  
|`=Fields(Parameters!` *\<NomeParametro>* `.Value).Value`|Restituisce il valore del campo il cui nome è uguale a quello del parametro.|  
  
 Per altre informazioni sull'uso dei parametri in un filtro, vedere [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md).  
  
##  <a name="Multi"></a> Utilizzo di un parametro multivalore in un'espressione  
 Nella tabella seguente sono riportati esempi della sintassi da utilizzare quando si include in un'espressione un riferimento a un parametro multivalore di un tipo di dati qualsiasi.  
  
|Esempio|Descrizione|  
|-------------|-----------------|  
|`=Parameters!` *\<NomeParametroMultivalore>* `.IsMultiValue`|Restituisce **True** o **False**.<br /><br /> Verifica se un parametro è multivalore. Se è **True**, il parametro è multivalore ed è costituito da una raccolta di oggetti. Se è **False**, il parametro è a valore singolo ed è costituito da un solo oggetto.|  
|`=Parameters!` *\<NomeParametroMultivalore>* `.Count`|Restituisce un valore intero.<br /><br /> Fa riferimento al numero di valori. Per un parametro a valore singolo, il conteggio è sempre 1. Per un parametro multivalore, il conteggio è 0 o maggiore di zero.|  
|`=Parameters!` *\<NomeParametroMultivalore>* `.Value(0)`|Restituisce il primo valore di un parametro multivalore.|  
|`=Parameters!` *\<NomeParametroMultivalore>* `.Value(Parameters!` *\<NomeParametroMultivalore>* `.Count-1)`|Restituisce l'ultimo valore di un parametro multivalore.|  
|`=Split("Value1,Value2,Value3",",")`|Restituisce una matrice di valori.<br /><br /> Creare una matrice di valori per un parametro multivalore di tipo **Stringa** . È possibile utilizzare qualsiasi delimitatore nel secondo parametro per dividere. È possibile utilizzare questa espressione per impostare i valori predefiniti di un parametro multivalore oppure creare un parametro multivalore da inviare a un sottoreport o a un report drill-through.|  
|`=Join(Parameters!` *\<NomeParametroMultivalore>* `.Value,", ")`|Restituisce un oggetto **Stringa** costituito da un elenco di valori delimitati da virgole in un parametro multivalore. È possibile utilizzare qualsiasi delimitatore nel secondo parametro per unire.|  
  
 Per altre informazioni sull'uso dei parametri in un filtro, vedere [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Filtri di uso comune &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [Aggiungere, modificare o eliminare un parametro di report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiungere un parametro al report &#40;Generatore report&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Esercitazioni di Generatore report](../../reporting-services/report-builder-tutorials.md)   
 [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)  
  
  
