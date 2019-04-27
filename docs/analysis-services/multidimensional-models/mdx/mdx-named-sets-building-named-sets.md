---
title: Creazione di set denominati in MDX (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b893dcd86ffcfa68c55057796c431e694903c46a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740061"
---
# <a name="mdx-named-sets---building-named-sets"></a>Set denominati MDX - creazione di set denominati
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Un'espressione set può essere costituita da una dichiarazione lunga e complessa e risultare pertanto difficile da seguire o comprendere oppure essere utilizzata con tale frequenza che la presenza di definizioni ripetute del set può creare confusione. Per semplificare l'utilizzo di espressioni lunghe, complesse o usate di frequente, le espressioni MDX (Multidimensional Expressions) consentono di definire un'espressione di questo tipo come *set denominato*.  
  
 Un set denominato è essenzialmente un'espressione set a cui è stato assegnato un alias. Un set denominato può incorporare qualsiasi funzione o membro che è normalmente possibile incorporare in un set. Poiché in MDX gli alias dei set denominati vengono gestiti come espressioni set, è possibile utilizzare tali alias in tutte le situazioni in cui è consentito utilizzare un'espressione set.  
  
 Un set denominato può essere definito con uno dei contesti seguenti:  
  
-   **Ambito query** Per creare un set denominato definito come parte di una query MDX, pertanto con ambito limitato alla query, è necessario usare la parola chiave WITH. Tale set denominato può essere quindi utilizzato in un'istruzione MDX SELECT. In questo modo il set denominato creato utilizzando la parola chiave WITH può essere modificato senza alterare l'istruzione SELECT.  
  
     Per altre informazioni sull'uso della parola chiave WITH per la creazione di set denominati, vedere [Creazione di set denominati con ambito query &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md).  
  
-   **Ambito sessione** Per creare un set denominato con ambito più ampio rispetto al contesto della query, ovvero con ambito corrispondente alla durata della sessione MDX, è possibile usare l'istruzione CREATE SET. Un set denominato definito utilizzando un'istruzione CREATE SET è disponibile per tutte le query MDX in tale sessione. L'istruzione CREATE SET risulta utile, ad esempio, in un'applicazione client che riutilizza in modo consistente un set in vari tipi di query.  
  
     Per altre informazioni sull'uso dell'istruzione CREATE SET per la creazione di set denominati in una sessione, vedere [Creazione di set denominati con ambito sessione &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-session-scoped-named-sets.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione SELECT &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)   
 [Istruzione CREATE SET &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-set.md)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
