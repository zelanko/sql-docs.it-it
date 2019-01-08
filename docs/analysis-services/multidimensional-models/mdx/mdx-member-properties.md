---
title: Uso delle proprietà dei membri (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7876031fddb74115fd1fe412f4c8a9d9aacdb054
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53216040"
---
# <a name="mdx-member-properties"></a>Proprietà dei membri MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Le proprietà dei membri contengono informazioni di base su ogni membro di ogni tupla. Tali informazioni di base includono il nome del membro, il livello padre, il numero di elementi figli e così via. Le proprietà dei membri sono disponibili per tutti i membri a un livello specifico. Per quanto riguarda l'organizzazione, le proprietà dei membri vengono gestite come dati organizzati a livello di dimensione, archiviati in una singola dimensione.  
  
> [!NOTE]
>  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]le proprietà dei membri sono dette relazioni tra attributi. Per altre informazioni, vedere [Relazioni tra attributi](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
 Le proprietà dei membri possono essere *intrinseche* o *personalizzate*:  
  
 Proprietà intrinseche dei membri  
 Tutti i membri supportano le proprietà intrinseche dei membri, ad esempio il valore formattato di un membro, mentre per le dimensioni e i livelli sono disponibili ulteriori proprietà intrinseche dei membri per livelli e dimensioni, quale l'ID di un membro.  
  
 Per altre informazioni, vedere [Proprietà intrinseche dei membri &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md).  
  
 Proprietà dei membri definite dall'utente  
 Ai membri sono spesso associate proprietà aggiuntive. Il livello Products, ad esempio, può includere le proprietà SKU, SRP, Weight e Volume per ogni prodotto. Tali proprietà non sono membri, ma includono informazioni aggiuntive sui membri del livello Products.  
  
 Per altre informazioni, vedere [Proprietà dei membri definite dall'utente &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
 Sia le proprietà intrinseche dei membri che quelle definite dall'utente possono essere recuperate usando la parola chiave **PROPERTIES** o la funzione [Properties](../../../mdx/properties-mdx.md).  
  
## <a name="using-the-properties-keyword"></a>Utilizzo della parola chiave PROPERTIES  
 La parola chiave **PROPERTIES** specifica le proprietà dei membri che devono essere usate per una determinata dimensione dell'asse. La parola chiave **PROPERTIES** viene inserita nella clausola `<axis specification>` dell'istruzione MDX [SELECT](../../../mdx/mdx-data-manipulation-select.md) :  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
```  
  
 La clausola `<axis_specification>` include la clausola facoltativa `<dim_props>`, come illustrato nella sintassi seguente:  
  
```  
<axis_specification> ::= <set> [<dim_props>] ON <axis_name>  
```  
  
> [!NOTE]  
>  Per altre informazioni sui valori di `<set>` e `<axis_name>`, vedere [Impostazione del contenuto di un asse della query &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
 La clausola `<dim_props>` consente di eseguire query sulle proprietà di dimensioni, livelli e membri usando la parola chiave **PROPERTIES**. Il formato della clausola `<dim_props>` è illustrato nella sintassi seguente:  
  
```  
<dim_props> ::= [DIMENSION] PROPERTIES <property> [,<property>...]  
```  
  
 Il dettaglio della sintassi di `<property>` dipende dalla proprietà su cui viene eseguita la query:  
  
-   Le proprietà dei membri intrinseche e sensibili al contesto devono essere precedute dal nome della dimensione o del livello. Le proprietà dei membri intrinseche e non sensibili al contesto non possono essere invece qualificate dal nome della dimensione o del livello. Per altre informazioni sull'uso della parola chiave **PROPERTIES** con le proprietà intrinseche dei membri, vedere [Proprietà intrinseche dei membri &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md).  
  
-   Le proprietà dei membri definite dall'utente devono essere precedute dal nome del livello in cui si trovano. Per altre informazioni sull'uso della parola chiave **PROPERTIES** con proprietà dei membri definite dall'utente, vedere [Proprietà dei membri definite dall'utente &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione e utilizzo di valori di proprietà &#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)  
  
  
