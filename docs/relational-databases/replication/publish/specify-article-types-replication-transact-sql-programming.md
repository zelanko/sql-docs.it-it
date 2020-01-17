---
title: Specificare i tipi di articolo (SP di replica)
description: Usare le stored procedure di replica per specificare a livello di programmazione un tipo di articolo quando si definisce un articolo per la replica SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- stored procedures [SQL Server replication], publishing
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3adcfa7c18259df1b063ff95f86d4f7721b45091
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321192"
---
# <a name="specify-article-types-replication-transact-sql-programming"></a>Impostazione dei tipi di articolo (programmazione Transact-SQL della replica)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  I tipi di articolo predefiniti per la replica sono gli articoli di tabella, ma è possibile pubblicare altri oggetti di database come articoli, tra cui viste, stored procedure, funzioni definite dall'utente ed esecuzione di stored procedure. È possibile utilizzare le stored procedure di replica per specificare a livello di programmazione un tipo di articolo mentre viene definito. Le stored procedure utilizzate dipendono dal tipo di replica e dal tipo di articolo.  
  
> [!NOTE]  
>  La designazione di solo schema durante la definizione di articoli di tabelle, viste e stored procedure indica che verrà replicata solo la definizione dell'oggetto.  
  
### <a name="to-publish-a-table-article-in-a-transactional-or-snapshot-publication"></a>Per pubblicare un articolo di tabella in una pubblicazione transazionale o snapshot  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Specificare uno dei valori seguenti per `@type` in modo da definire il tipo di articolo:  
  
    -   `logbased`: articolo di tabella basato su log, che rappresenta l'impostazione predefinita per la replica transazionale e snapshot. Con la replica vengono automaticamente generate la stored procedure utilizzata per il filtro orizzontale e la vista che definisce un articolo con filtro verticale.  
  
    -   `logbased manualfilter`: articolo basato su log con filtro orizzontale in cui la stored procedure usata per applicare il filtro orizzontale viene creata e definita manualmente dall'utente e specificata per `@filter`. Per altre informazioni, vedere [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -  `logbased manualview`: articolo basato su log con filtro verticale in cui la vista che definisce l'articolo con filtro verticale viene creata e definita dall'utente e specificata per `@sync_object`. Per ulteriori informazioni, vedere [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) e [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   `logbased manualboth`: articolo basato su log con filtro orizzontale e verticale in cui sia la stored procedure usata per applicare il filtro orizzontale sia la vista che definisce l'articolo con filtro verticale vengono create e definite dall'utente e specificate rispettivamente per `@filter` e `@sync_object`. Per ulteriori informazioni, vedere [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) e [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     In questo modo viene definito un nuovo articolo per la pubblicazione. Per altre informazioni, vedere [definire un articolo](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Per gli articoli `logbased manualboth` e `logbased manualfilter`, eseguire [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) per generare la stored procedure di filtro per un articolo con filtro orizzontale. Per altre informazioni, vedere [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Per gli articoli `logbased manualboth`, `logbased manualview` e `logbased manualfilter`, eseguire [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) per generare la vista che definisce l'articolo con filtro verticale. Per altre informazioni, vedere [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  

### <a name="to-publish-a-view-or-indexed-view-article-in-a-transactional-or-snapshot-publication"></a>Per pubblicare un articolo di vista o di vista indicizzata in una pubblicazione transazionale o snapshot  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Specificare uno dei valori seguenti per `@type` in modo da definire il tipo di articolo:  
  
    -   **indexed view logbased** : articolo di vista indicizzata basato su log. Con la replica vengono automaticamente generate la stored procedure utilizzata per il filtro orizzontale e la vista che definisce un articolo con filtro verticale.  
  
    -   **view schema only** : articolo di vista di solo schema. È necessario replicare anche la tabella di base.  
  
    -   **indexed view schema only** : articolo di vista indicizzata di solo schema. È necessario replicare anche la tabella di base.  
  
    -   **indexed view logbased manualfilter**: articolo di vista indicizzata basato su log con filtro orizzontale in cui la stored procedure usata per applicare il filtro orizzontale viene creata e definita manualmente dall'utente e specificata per `@filter`. Per altre informazioni, vedere [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
    -   **indexed view logbased manualview**: articolo di vista indicizzata basato su log con filtro in cui la vista che definisce un articolo con filtro verticale viene creata e definita dall'utente e specificata per `@sync_object`. Per ulteriori informazioni, vedere [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) e [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
    -   **indexed view logbased manualboth**: articolo di vista indicizzata basato su log con filtro in cui sia la stored procedure usata per applicare il filtro orizzontale sia la vista che definisce un articolo con filtro verticale vengono create e definite dall'utente e specificate rispettivamente per `@filter` e `@sync_object`. Per ulteriori informazioni, vedere [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) e [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
     In questo modo viene definito un nuovo articolo per la pubblicazione. Per altre informazioni, vedere [definire un articolo](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Per gli articoli **logbased manualboth** e **logbased manualfilter** , eseguire [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) per generare la stored procedure di filtro per un articolo con filtro orizzontale. Per altre informazioni, vedere [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
3.  Per gli articoli **logbased manualboth**, **logbased manualview**e **logbased manualfilter** , eseguire [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) per generare la vista che definisce l'articolo con filtro verticale. Per altre informazioni, vedere [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
### <a name="to-publish-a-stored-procedure-stored-procedure-execution-or-user-defined-function-article-in-a-transactional-or-snapshot-publication"></a>Per pubblicare un articolo di stored procedure, esecuzione di stored procedure o funzione definita dall'utente in una pubblicazione transazionale o snapshot  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Specificare uno dei valori seguenti per `@type` in modo da definire il tipo di articolo:  
  
    -   **proc schema only** : articolo di stored procedure di solo schema.  
  
    -   **proc exec** : replica l'esecuzione della stored procedure in tutti i Sottoscrittori dell'articolo. Per altre informazioni, vedere [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **serializable proc exec** : replica l'esecuzione della stored procedure solo se viene eseguita nel contesto di una transazione serializzabile. Per altre informazioni, vedere [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
    -   **func schema only** : articolo di funzione definita dall'utente di solo schema.  
  
     In questo modo viene definito un nuovo articolo per la pubblicazione. Per altre informazioni, vedere [definire un articolo](../../../relational-databases/replication/publish/define-an-article.md).  
  
### <a name="to-publish-a-table-or-view-article-in-a-merge-publication"></a>Per pubblicare un articolo di tabella o vista in una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Specificare uno dei valori seguenti per `@type` in modo da definire il tipo di articolo:  
  
    -   **table** : articolo di tabella.  
  
    -   **indexed view schema only** : articolo di vista indicizzata di solo schema.  
  
    -   **view schema only** : articolo di vista di solo schema.  
  
     In questo modo viene definito un nuovo articolo per la pubblicazione. Per altre informazioni, vedere [definire un articolo](../../../relational-databases/replication/publish/define-an-article.md).  
  
### <a name="to-publish-a-stored-procedure-or-user-defined-function-article-in-a-merge-publication"></a>Per pubblicare un articolo di stored procedure o funzione definita dall'utente in una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Specificare uno dei valori seguenti per `@type` in modo da definire il tipo di articolo:  
  
    -   **func schema only** : articolo di funzione definita dall'utente di solo schema.  
  
    -   **proc schema only** : articolo di stored procedure di solo schema.  
  
     In questo modo viene definito un nuovo articolo per la pubblicazione. Per altre informazioni, vedere [definire un articolo](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Pubblicare dati e oggetti di database](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
