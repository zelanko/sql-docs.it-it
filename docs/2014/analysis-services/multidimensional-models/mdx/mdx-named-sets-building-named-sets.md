---
title: Creazione di set denominati in MDX (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], named sets
- named sets [MDX]
- sets [MDX]
- MDX [Analysis Services], named sets
- queries [MDX], named sets
- set expressions [MDX]
ms.assetid: 213b0035-e96d-4ba0-83f2-ded206905603
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98d363ab09e75905b13503687fe425a981c790e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074152"
---
# <a name="building-named-sets-in-mdx-mdx"></a>Compilazione di set denominati in MDX (MDX)
  Un'espressione set può essere costituita da una dichiarazione lunga e complessa e risultare pertanto difficile da seguire o comprendere oppure essere utilizzata con tale frequenza che la presenza di definizioni ripetute del set può creare confusione. Per semplificare l'utilizzo di espressioni lunghe, complesse o usate di frequente, le espressioni MDX (Multidimensional Expressions) consentono di definire un'espressione di questo tipo come *set denominato*.  
  
 Un set denominato è essenzialmente un'espressione set a cui è stato assegnato un alias. Un set denominato può incorporare qualsiasi funzione o membro che è normalmente possibile incorporare in un set. Poiché in MDX gli alias dei set denominati vengono gestiti come espressioni set, è possibile utilizzare tali alias in tutte le situazioni in cui è consentito utilizzare un'espressione set.  
  
 Un set denominato può essere definito con uno dei contesti seguenti:  
  
-   **Ambito query** Per creare un set denominato definito come parte di una query MDX, pertanto con ambito limitato alla query, è necessario usare la parola chiave WITH. Tale set denominato può essere quindi utilizzato in un'istruzione MDX SELECT. In questo modo il set denominato creato utilizzando la parola chiave WITH può essere modificato senza alterare l'istruzione SELECT.  
  
     Per altre informazioni sull'uso della parola chiave WITH per la creazione di set denominati, vedere [Creazione di set denominati con ambito query &#40;MDX&#41;](mdx-named-sets-creating-query-scoped-named-sets.md).  
  
-   **Ambito sessione** Per creare un set denominato con ambito più ampio rispetto al contesto della query, ovvero con ambito corrispondente alla durata della sessione MDX, è possibile usare l'istruzione CREATE SET. Un set denominato definito utilizzando un'istruzione CREATE SET è disponibile per tutte le query MDX in tale sessione. L'istruzione CREATE SET risulta utile, ad esempio, in un'applicazione client che riutilizza in modo consistente un set in vari tipi di query.  
  
     Per altre informazioni sull'uso dell'istruzione CREATE SET per la creazione di set denominati in una sessione, vedere [Creazione di set denominati con ambito sessione &#40;MDX&#41;](mdx-named-sets-creating-session-scoped-named-sets.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione SELECT &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [Istruzione CREATE SET &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-set)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
