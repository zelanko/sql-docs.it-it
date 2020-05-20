---
title: Nuovo punto di interruzione full-text (pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplist.general.f1
ms.assetid: 97f8e82d-82ab-4525-91c9-1ee3ae217309
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1dc58f006d1e37885418dfb923c6c7cc7563d018
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000831"
---
# <a name="new-full-text-stoplist-general-page"></a>Nuovo elenco di parole non significative full-text (pagina Generale)
  Utilizzare questa finestra di dialogo per creare un elenco di parole non significative full-text. Un *elenco di parole non significative* è un set di parole di uso comune, denominate *parole non significative*, omesse dall'indicizzazione full-text per tabelle che utilizzano l'elenco di parole non significative. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../relational-databases/search/full-text-search.md).  
  
 **Per utilizzare SQL Server Management Studio per la creazione di un elenco di parole non significative**  
  
-   [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>Opzioni  
 **Nome elenco di parole non significative full-text**  
 Consente di immettere il nome dell'elenco di parole non significative full-text.  
  
 **Proprietario**  
 Consente di specificare il proprietario dell'elenco di parole non significative full-text. Se si desidera impostare se stessi, ovvero l'utente corrente, come proprietario, lasciare vuoto questo campo.  
  
 Per specificare un utente diverso, fare clic sul pulsante Sfoglia.  
  
### <a name="create-stoplist-options"></a>Opzioni di creazione di elenchi di parole non significative  
 Fare clic su una delle opzioni di creazione seguenti:  
  
 **Creare un elenco di parole non significative vuoto**  
 Il nuovo elenco di parole non significative non conterrà alcuna parola non significativa.  
  
 **Creare un elenco di parole non significative da un elenco di parole non significative di sistema**  
 Il nuovo elenco di parole non significative viene creato dall'elenco di parole non significative esistente per impostazione predefinita nel [Database Resource](../relational-databases/databases/resource-database.md).  
  
 **Creare un elenco di parole non significative da un elenco di parole non significative full-text esistente**  
 Il nuovo elenco di parole non significative viene creato copiando un elenco di parole non significative esistente.  
  
 **Database di origine**  
 Specifica il nome del database a cui appartiene l'elenco di parole non significative esistente. Per impostazione predefinita, è selezionato il database corrente. Se si desidera, selezionare un database diverso nella casella di riepilogo.  
  
 **Elenco di parole non significative di origine**  
 Specifica il nome di un elenco di parole non significative esistente. Nell'elenco di elenchi di parole non significative disponibili selezionare quello da utilizzare come origine. Gli elenchi di parole non significative disponibili sono elencati nell'ordine in cui vengono visualizzati in Esplora oggetti.  
  
 Se qualsiasi lingua specificata nelle parole non significative dell'elenco di parole non significative di origine non è registrata nel database corrente, CREATE FULLTEXT STOPLIST ha esito positivo, ma vengono restituiti avvisi e le parole non significative corrispondenti non vengono aggiunte.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER FULLTEXT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [CREAZIONE di un &#40;di parole non significative full-text&#41;Transact-SQL](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT elenco di parole non significative &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)   
 [Configurare e gestire parole non significative e elenchi per la ricerca full-text](../relational-databases/search/full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)  
  
  
