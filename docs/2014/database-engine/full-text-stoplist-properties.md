---
title: Le proprietà di parole non significative Full-Text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplistproperties.general.f1
- sql12.swb.fulltextsearch.ftstoplistproperties.schedule.f1
ms.assetid: 2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 4cfdd308ab7488633721ddaac55d3d926a276b0d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779408"
---
# <a name="full-text-stoplist-properties"></a>Proprietà elenco di parole non significative full-text
  Utilizzare questa finestra di dialogo per aggiungere o eliminare singole parole non significative, eliminare tutte le parole non significative per una lingua specifica oppure cancellare l'elenco di parole non significative corrente. Una parola non significativa è una parola di uso comune inclusa in un elenco di parole non significative. Le parole contenute in un elenco di questo tipo vengono omesse dall'indicizzazione full-text nelle tabelle che utilizzano l'elenco stesso. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../relational-databases/search/full-text-search.md).  
  
 **Usare SQL Server Management Studio per modificare le proprietà di parole non significative**  
  
-   [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>Opzioni  
 **Azione**  
 Consente di specificare l'azione che si desidera eseguire.  
  
 **Aggiungi parola non significativa**  
 Consente di aggiungere una parola di uso comune all'elenco di parole non significative.  
  
 **Elimina parola non significativa**  
 Consente di eliminare una parola non significativa dall'elenco.  
  
 **Elimina tutte le parole non significative**  
 Consente di eliminare tutte le parole non significative per una lingua specifica.  
  
 **Cancella elenco di parole non significative**  
 Consente di cancellare l'elenco di parole non significative eliminando tutte le parole non significative per tutte le lingue.  
  
 **Stopword**  
 Se è stato selezionato **Aggiungi parola non significativa** oppure **Elimina parola non significativa**, immettere la parola non significativa nel **parola non significativa** campo. Una nuova parola non significativa deve essere univoca, ovvero non ancora inclusa nell'elenco di parole non significative per la lingua selezionata.  
  
 **Lingua full-text**  
 Se è stato selezionato **Aggiungi parola non significativa**, **Elimina parola non significativa**, o **Elimina tutte le parole non significative**, selezionare la lingua della parola non significativa o le parole non significative dall'elenco. Nella casella sono elencate tutte le lingue full-text supportate dall'istanza del server.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)   
 [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../relational-databases/search/full-text-search.md)   
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  
