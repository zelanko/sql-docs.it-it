---
title: Modifica dei dati (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f4fdaf60309d09a706fea552722017756b7945d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208766"
---
# <a name="mdx-data-modification---modifying-data"></a>Modifica dei dati MDX - modifica dei dati
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Oltre che per recuperare e gestire i dati di dimensioni e cubi, il linguaggio MDX (Multidimensional Expressions) può essere usato anche per aggiornarli o eseguirne il *writeback* . Tali aggiornamenti possono essere temporanei, come nel caso delle analisi speculative, o di simulazione, oppure permanenti, come nel caso in cui le modifiche dipendono dall'analisi dei dati.  
  
 Gli aggiornamenti possono essere eseguiti a livello di dimensione o di cubo:  
  
 **Writeback delle dimensioni**  
 È possibile usare l'istruzione [ALTER CUBE Statement (MDX)](../../../mdx/mdx-data-definition-alter-cube.md) per modificare i dati di una dimensione abilitata per la scrittura e [REFRESH CUBE Statement (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) per riflettere l'eliminazione, la creazione e l'aggiornamento dei valori degli attributi. L'istruzione ALTER CUBE può essere inoltre utilizzata per svolgere operazioni complesse, ad esempio l'eliminazione di un intero sottoalbero di una gerarchia e la promozione dei figli di un membro eliminato.  
  
 **Writeback dei cubi**  
 È possibile usare l'istruzione [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) per aggiornare un cubo abilitato per la scrittura. L'istruzione UPDATE CUBE consente di aggiornare una tupla con un valore specifico. È possibile usare l'istruzione [REFRESH CUBE Statement (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) per aggiornare i dati in una sessione client con i dati aggiornati del server.  
  
 Per altre informazioni, vedere [Utilizzo dei writeback dei cubi &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-using-cube-writebacks.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
