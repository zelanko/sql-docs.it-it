---
title: Proprietà indice full-text (pagina colonne) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.columns.f1
ms.assetid: 75e52edb-0d07-4393-9345-8b5af4561e35
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f1b842f8fe4e2a5c3adc489df35e20c58000a69d
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000917"
---
# <a name="full-text-index-properties-columns-page"></a>Proprietà indice full-text (pagina Colonne)
  **Per visualizzare o modificare le proprietà di un indice full-text**  
  
-   [Gestione di indici full-text.](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Indice univoco**  
 Selezionare un indice dall'elenco a discesa. L'indice deve essere univoco, a colonna singola, che non ammette valori Null.  
  
 **Selezionare le colonne idonee per l'indicizzazione full-text**  
 Nella griglia vengono visualizzate le colonne della tabella disponibili per l'indice full-text corrente. Le colonne con indicizzazione full-text sono selezionate. Se si desidera, è possibile selezionare colonne aggiuntive cui applicare l'indicizzazione full-text.  
  
> [!IMPORTANT]  
>  Prima di fare clic su OK, verificare che sia selezionata almeno una colonna.  
  
|||  
|-|-|  
|**Colonne disponibili**|Nome della colonna.|  
|**Lingua per il Word breaker**|Lingua i cui word breaker e stemmer eseguono l'analisi linguistica su tutti i dati con indicizzazione full-text.<br /><br /> Per ulteriori informazioni, vedere [configurare e gestire Word breaker e stemmer per la ricerca](../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) e [scegliere una lingua durante la creazione di un indice full-text](../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).|  
|**Type**|Nome della colonna di tabella contenente il tipo di documento della colonna selezionata. Questa proprietà è di sola lettura.|  
|**Semantica statistica**|Consente di selezionare se abilitare l'indicizzazione semantica per la colonna selezionata. Per altre informazioni, vedere [Ricerca semantica &#40;SQL Server&#41;](../relational-databases/search/semantic-search-sql-server.md).<br /><br /> Se si seleziona una lingua in **Lingua** prima di selezionare **Semantica statistica**e alla lingua selezionata non è associato alcun modello di lingua semantico, la casella di controllo **Semantica statistica** è disabilitata. Se si seleziona **Semantica statistica** prima di selezionare una lingua in **Lingua**, le lingue disponibili nella casella combinata a discesa saranno limitate a quelle per cui è disponibile un modello di lingua semantico.|  
  
## <a name="see-also"></a>Vedere anche  
 [Popolamento degli indici full-text](../relational-databases/search/populate-full-text-indexes.md)  
  
  
