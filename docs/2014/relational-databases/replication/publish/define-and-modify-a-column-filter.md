---
title: Definire e modificare un filtro colonne | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], column
- modifying filters, column
- modifying filters
- column filters [SQL Server replication]
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7e00ceeae68ccc791c3680e029e13844fa6ec683
ms.sourcegitcommit: 0d89bcaebdf87db3bd26db2ca263be9c671b0220
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2019
ms.locfileid: "68731065"
---
# <a name="define-and-modify-a-column-filter"></a>Definizione e modifica di un filtro colonne
  In questo argomento viene descritto come definire e modificare un filtro colonne in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
-   **Per definire e modificare un filtro colonne, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Alcune colonne non possono essere filtrate. Per altre informazioni, vedere [Filtrare i dati pubblicati](filter-published-data.md). Se si modifica un filtro di colonna dopo l'inizializzazione delle sottoscrizioni, dopo la modifica è necessario generare un nuovo snapshot e reinizializzare tutte le sottoscrizioni. Per altre informazioni sui requisiti per la modifica delle proprietà, vedere [Modificare le proprietà di pubblicazioni e articoli](change-publication-and-article-properties.md).  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Definire i filtri colonne nella pagina **Articoli** della Creazione guidata nuova pubblicazione. Per altre informazioni sull'uso della Creazione guidata nuova pubblicazione, vedere [Creare una pubblicazione](create-a-publication.md).  
  
 Definire e modificare i filtri di colonna nella pagina **Articoli** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** . Per altre informazioni sulla modifica delle proprietà di pubblicazione, vedere [Visualizzare e modificare le proprietà della pubblicazione](view-and-modify-publication-properties.md).  
  
#### <a name="to-define-a-column-filter"></a>Per definire un filtro colonne  
  
1.  Nella pagina **Articoli** della Creazione guidata nuova pubblicazione espandere la tabella da filtrare nel riquadro **Oggetti da pubblicare** .  
  
2.  Deselezionare la casella di controllo accanto a ogni colonna che si desidera filtrare.  
  
#### <a name="to-modify-column-filtering"></a>Per modificare l'applicazione di filtri di colonna  
  
1.  Nella pagina **Articoli** della finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** espandere la tabella da filtrare nel riquadro **Oggetti da pubblicare**.  
  
2.  Deselezionare la casella di controllo accanto a ogni colonna che si desidera filtrare e verificare che la casella di controllo sia selezionata per ogni colonna da includere nell'articolo.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 Durante la creazione di articoli di tabella è possibile definire le colonne da includere nell'articolo e modificare le colonne dopo aver definito l'articolo. È possibile creare e modificare a livello di programmazione le colonne filtrate tramite le stored procedure di replica.  
  
> [!NOTE]  
>  Nelle procedure seguenti si presuppone che la tabella sottostante non sia modificata. Per informazioni sulla replica di modifiche DDL (Data Definition Language) in tabelle pubblicate, vedere [Apportare modifiche allo schema nei database di pubblicazione](make-schema-changes-on-publication-databases.md).  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>Per definire un filtro di colonna per un articolo pubblicato di una pubblicazione snapshot o transazionale  
  
1.  Definire l'articolo da filtrare. Per altre informazioni, vedere [Define an Article](define-an-article.md).  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql). Verranno definite le colonne da includere o rimuovere dall'articolo.  
  
    -   Se si intende pubblicare solo alcune colonne di una tabella contenente molte colonne, eseguire [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) una volta per ogni colonna da aggiungere. Specificare il nome  **\@** della colonna e il valore **Add** per  **\@Operation**.  
  
    -   Se si pubblica la maggior parte delle colonne di una tabella con molte colonne, eseguire [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql), specificando il valore **null** per  **\@Column** e il valore **Add** per  **\@Operation** per aggiungere tutte le colonne. Eseguire quindi [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql), una volta per ogni colonna da escludere, specificando il valore **Drop** for  **\@Operation** e il nome della colonna esclusa per  **\@Column**.  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql). Specificare il nome della pubblicazione  **\@** per la pubblicazione e il nome dell'articolo filtrato per  **\@l'articolo**. Verranno creati gli oggetti di sincronizzazione per l'articolo filtrato.  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>Per modificare un filtro colonne in modo da includere colonne aggiuntive per un articolo pubblicato di una pubblicazione snapshot o transazionale  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) una volta per ogni colonna da aggiungere. Specificare il nome  **\@** della colonna e il valore **Add** per  **\@Operation**.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql). Specificare il nome della pubblicazione  **\@** per la pubblicazione e il nome dell'articolo filtrato per  **\@l'articolo**. Se la pubblicazione include sottoscrizioni esistenti, specificare il valore **1** per  **\@change_active**. Verranno creati nuovamente gli oggetti di sincronizzazione per l'articolo filtrato.  
  
3.  Rieseguire il processo dell'agente snapshot per la pubblicazione per generare uno snapshot aggiornato.  
  
4.  Reinizializzazione delle sottoscrizioni. Per altre informazioni, vedere [Reinizializzare le sottoscrizioni](../reinitialize-subscriptions.md).  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>Per modificare un filtro colonne in modo da rimuovere colonne per un articolo pubblicato di una pubblicazione snapshot o transazionale  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) una volta per ogni colonna da rimuovere. Specificare il nome  **\@** della colonna e il valore **Drop** per  **\@Operation**.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql). Specificare il nome della pubblicazione  **\@** per la pubblicazione e il nome dell'articolo filtrato per  **\@l'articolo**. Se la pubblicazione include sottoscrizioni esistenti, specificare il valore **1** per  **\@change_active**. Verranno creati nuovamente gli oggetti di sincronizzazione per l'articolo filtrato.  
  
3.  Rieseguire il processo dell'agente snapshot per la pubblicazione per generare uno snapshot aggiornato.  
  
4.  Reinizializzazione delle sottoscrizioni. Per altre informazioni, vedere [Reinizializzare le sottoscrizioni](../reinitialize-subscriptions.md).  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-merge-publication"></a>Per definire un filtro di colonna per un articolo pubblicato di una pubblicazione di tipo merge  
  
1.  Definire l'articolo da filtrare. Per altre informazioni, vedere [definire un articolo](define-an-article.md).  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql). Verranno definite le colonne da includere o rimuovere dall'articolo.  
  
    -   Se si intende pubblicare solo alcune colonne di una tabella contenente molte colonne, eseguire [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) una volta per ogni colonna da aggiungere. Specificare il nome  **\@** della colonna e il valore **Add** per  **\@Operation**.  
  
    -   Se si pubblica la maggior parte delle colonne di una tabella con molte colonne, eseguire [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql), specificando il valore **null** per  **\@Column** e il valore **Add** per  **\@Operation** per aggiungere all. colonne. Eseguire quindi [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql), una volta per ogni colonna da escludere, specificando il valore **Drop** for  **\@Operation** e il nome della colonna esclusa per  **\@Column**.  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-merge-publication"></a>Per modificare un filtro colonne in modo da includere colonne aggiuntive per un articolo pubblicato di una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) una volta per ogni colonna da aggiungere. Specificare  **\@** il nome della colonna, il valore **Add** per  **\@Operation** e il valore **1** sia  **\@per force_invalidate_snapshot** che  **\@per force_reinit_ sottoscrizione**.  
  
2.  Rieseguire il processo dell'agente snapshot per la pubblicazione per generare uno snapshot aggiornato.  
  
3.  Reinizializzazione delle sottoscrizioni. Per altre informazioni, vedere [Reinizializzare le sottoscrizioni](../reinitialize-subscriptions.md).  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-merge-publication"></a>Per modificare un filtro colonne in modo da rimuovere colonne per un articolo pubblicato di una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) una volta per ogni colonna da rimuovere. Specificare  **\@** il nome della colonna, il valore **Drop** per  **\@Operation** e il valore **1** sia  **\@per force_invalidate_snapshot** che  **\@per force_reinit_ sottoscrizione**.  
  
2.  Rieseguire il processo dell'agente snapshot per la pubblicazione per generare uno snapshot aggiornato.  
  
3.  Reinizializzazione delle sottoscrizioni. Per altre informazioni, vedere [Reinizializzare le sottoscrizioni](../reinitialize-subscriptions.md).  
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
 In questo esempio di replica transazionale la colonna `DaysToManufacture` viene rimossa da un articolo basato sulla tabella `Product` .  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createtranpub.sql#sp_addtranarticle)]  
  
 In questo esempio di replica di tipo merge la colonna `CreditCardApprovalCode` viene rimossa da un articolo basato sulla tabella `SalesOrderHeader` .  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergearticle)]  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare le proprietà di pubblicazioni e articoli](change-publication-and-article-properties.md)   
 [Filtrare i dati pubblicati](filter-published-data.md)   
 [Filtrare i dati pubblicati per la replica di tipo merge](../merge/filter-published-data-for-merge-replication.md)  
  
  
