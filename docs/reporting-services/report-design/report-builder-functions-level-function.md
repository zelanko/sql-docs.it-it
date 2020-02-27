---
title: Funzione Level (Generatore report) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1e70847a25230be39166ac6fa489f1fdc3f23e43
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081244"
---
# <a name="report-builder-functions---level-function"></a>Funzioni di Generatore report - Funzione Level
  Restituisce il livello di nidificazione corrente in una gerarchia ricorsiva.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Level(scope)  
```  
  
#### <a name="parameters"></a>Parametri  
 *ambito*  
 (**String**) Facoltativo. Nome di un set di dati, gruppo o area dati che contiene gli elementi del report a cui applicare la funzione di aggregazione. Se si omette *scope* , viene usato l'ambito corrente.  
  
## <a name="return-type"></a>Tipo restituito  
 Restituisce un valore **Integer**. Se il parametro *scope* specifica un set di dati o un'area dati oppure un raggruppamento non ricorsivo, ovvero un raggruppamento privo dell'elemento **Parent** , **Level** restituirà 0. Se *scope* viene omesso, restituisce il livello dell'ambito corrente.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore restituito dalla funzione **Level** è a base zero, ovvero il primo livello di una gerarchia viene indicato con 0.  
  
 È possibile utilizzare la funzione **Level** per consentire l'applicazione dei rientri in una gerarchia ricorsiva, ad esempio un elenco di dipendenti.  
  
 Per altre informazioni sulle gerarchie ricorsive, vedere [Creazione di gruppi di gerarchie ricorsive &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Esempio  
 L'esempio di codice seguente consente di ottenere il livello di riga nel gruppo Employees:  
  
```  
=Level("Employees")  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
