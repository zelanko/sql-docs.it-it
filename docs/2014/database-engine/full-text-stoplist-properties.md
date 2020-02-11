---
title: Proprietà di parole non significative full-text | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779408"
---
# <a name="full-text-stoplist-properties"></a>Proprietà elenco di parole non significative full-text
  Utilizzare questa finestra di dialogo per aggiungere o eliminare singole parole non significative, eliminare tutte le parole non significative per una lingua specifica oppure cancellare l'elenco di parole non significative corrente. Una parola non significativa è una parola di uso comune inclusa in un elenco di parole non significative. Le parole contenute in un elenco di questo tipo vengono omesse dall'indicizzazione full-text nelle tabelle che utilizzano l'elenco stesso. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../relational-databases/search/full-text-search.md).  
  
 **Per utilizzare SQL Server Management Studio per modificare le proprietà dell'elenco di parole non significative**  
  
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
  
 **Parola non significativa**  
 Se è stata selezionata l'opzione **Aggiungi parola non significativa** o **Elimina parola non significativa**, immettere parola non significativa nel campo **parola non significativa** . Una nuova parola non significativa deve essere univoca, ovvero non ancora inclusa nell'elenco di parole non significative per la lingua selezionata.  
  
 **Lingua full-text**  
 Se è stata selezionata l'opzione **Aggiungi parola non significativa**, **Elimina parola non significativa**o **Elimina tutti i parole non significative**, selezionare la lingua di parola non significativa o parole non significative nella casella di riepilogo. Nella casella sono elencate tutte le lingue full-text supportate dall'istanza del server.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)   
 [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../relational-databases/search/full-text-search.md)   
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  
