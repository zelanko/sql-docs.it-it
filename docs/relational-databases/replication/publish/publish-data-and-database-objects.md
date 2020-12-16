---
title: Pubblicare dati e oggetti di database | Microsoft Docs
description: Questo articolo riepiloga le tabelle e altri oggetti di database che è possibile pubblicare per la replica in SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- user-defined types [SQL Server replication]
- articles [SQL Server replication], dropping
- objects [SQL Server replication]
- publications [SQL Server replication], creating
- merge replication [SQL Server replication], publications
- schema-only articles [SQL Server replication]
- publishing [SQL Server replication], database objects
- articles [SQL Server replication], defining
- publishing [SQL Server replication], functions
- replication [SQL Server], publications
- publishing [SQL Server replication], views
- tables [SQL Server replication]
- schemas [SQL Server replication]
- publishing [SQL Server replication], data
- schemas [SQL Server replication], publishing
- articles [SQL Server replication], stored procedures and
- publishing [SQL Server replication], tables
- alias data types [SQL Server replication]
- publications [SQL Server replication], deleting
- snapshot replication [SQL Server], publications
- articles [SQL Server replication], modifying
- transactional replication, publications
- publishing [SQL Server replication], stored procedures
- publishing [SQL Server replication]
- views [SQL Server replication]
- stored procedures [SQL Server replication], publishing
- publications [SQL Server replication], schema options
- articles [SQL Server replication], adding
- publications [SQL Server replication], modifying
- user-defined functions [SQL Server replication]
ms.assetid: d986032c-3387-4de1-a435-3ec5e82185a2
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 6f0302c5807a93fdac826bb67a85c8e4e3e4abb5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468972"
---
# <a name="publish-data-and-database-objects"></a>Pubblicazione di dati e oggetti di database
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Quando si crea una pubblicazione, è possibile scegliere le tabelle e gli altri oggetti di database che si desidera pubblicare. Tramite la replica è possibile pubblicare gli oggetti di database elencati di seguito.  
  
|Oggetto di database|Replica snapshot e replica transazionale|Replica di tipo merge|  
|---------------------|--------------------------------------------------------|-----------------------|  
|Tabelle|X|X|  
|Tabelle partizionate|X|X|  
|Stored procedure - definizione ([!INCLUDE[tsql](../../../includes/tsql-md.md)] e CLR)|X|X|  
|Stored procedure - esecuzione ([!INCLUDE[tsql](../../../includes/tsql-md.md)] e CLR)|X|no|  
|Viste|X|X|  
|Viste indicizzate|X|X|  
|Viste indicizzate come tabelle|X|no|  
|Tipi definiti dall'utente (CLR)|X|X|  
|Funzioni definite dall'utente ([!INCLUDE[tsql](../../../includes/tsql-md.md)] e CLR).|X|X|  
|Tipi di dati alias|X|X|  
|Indici full-text|X|X|  
|Oggetti dello schema (vincoli, indici, trigger DML dell'utente, proprietà estese e regole di confronto)|X|X|  
  
## <a name="creating-publications"></a>Creazione di pubblicazioni  
 Per creare una pubblicazione, si specificano le informazioni seguenti:  
  
-   Server di distribuzione.    
-   Percorso dei file di snapshot.    
-   Database di pubblicazione.    
-   Tipo di pubblicazione da creare (snapshot, transazionale, transazionale con sottoscrizioni aggiornabili o di tipo merge).    
-   Dati e oggetti di database (articoli) da includere nella pubblicazione.   
-   Filtri di colonna e filtri di riga statici per tutti i tipi di pubblicazioni, nonché filtri join e filtri di riga con parametri per le pubblicazioni di tipo merge.   
-   Pianificazione dell'agente snapshot.    
-   Account usati per l'esecuzione degli agenti seguenti: agente snapshot per tutte le pubblicazioni, agente di lettura log per tutte le pubblicazioni transazionali e agente di lettura coda per tutte le pubblicazioni transazionali che consentono sottoscrizioni aggiornabili.    
-   Nome e descrizione della pubblicazione.  
  
 Per informazioni sull'utilizzo di pubblicazioni, vedere gli argomenti seguenti:    
-   [Creare una pubblicazione](../../../relational-databases/replication/publish/create-a-publication.md)    
-   [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)    
-   [Visualizzare e modificare le proprietà della pubblicazione](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)    
-   [Visualizzare e modificare le proprietà degli articoli](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)    
-   [Eliminare una pubblicazione](../../../relational-databases/replication/publish/delete-a-publication.md)    
-   [Eliminare un articolo](../../../relational-databases/replication/publish/delete-an-article.md)  
  
> [!NOTE]  
>  L'eliminazione di un articolo o una pubblicazione non determina la rimozione di oggetti dal Sottoscrittore.  
  
## <a name="publishing-tables"></a>Pubblicazione di tabelle  
 L'oggetto più comunemente pubblicato è costituito da una tabella. È possibile utilizzare i collegamenti seguenti per ottenere informazioni aggiuntive sulle aree correlate alla pubblicazione di tabelle:  
  
-   [Filtrare i dati pubblicati](../../../relational-databases/replication/publish/filter-published-data.md)    
-   [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)
-   [Opzioni degli articoli per la replica di tipo merge](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)    
-   [Replicare colonne Identity](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
 Quando si pubblica una tabella per la replica, è possibile specificare gli oggetti dello schema da copiare nel Sottoscrittore, ad esempio l'integrità referenziale dichiarata (vincoli di chiave primaria, di riferimento o UNIQUE), indici, trigger DML dell'utente (i trigger DDL non possono essere replicati), proprietà estese e regole di confronto. Le proprietà estese vengono replicate solo nella sincronizzazione iniziale tra il server di pubblicazione e il Sottoscrittore. Se si aggiungono o si modificano proprietà estese dopo la sincronizzazione iniziale, le modifiche apportate non vengono replicate.  
  
 Per specificare le opzioni dello schema, vedere [Specificare le opzioni dello schema](../../../relational-databases/replication/publish/specify-schema-options.md) oppure <xref:Microsoft.SqlServer.Replication.Article.SchemaOption%2A>.  
  
### <a name="partitioned-tables-and-indexes"></a>Partitioned Tables and Indexes  
 La replica supporta la pubblicazione di tabelle e indici partizionati. Il livello di supporto dipende dal tipo di replica utilizzato, nonché dalle opzioni specificate per la pubblicazione e dagli articoli associati alle tabelle partizionate. Per altre informazioni, vedere [Replicare tabelle e indici partizionati](../../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
## <a name="publishing-stored-procedures"></a>Pubblicazione di stored procedure  
 Tutti i tipi di replica consentono di replicare definizioni di stored procedure, copiando CREATE PROCEDURE in ogni Sottoscrittore. In caso di stored procedure CLR (Common Language Runtime), viene inoltre copiato l'assembly associato. Le modifiche apportate alle procedure vengono replicate nei Sottoscrittori, mentre non vengono replicate le modifiche agli assembly associati.  
  
 Oltre alla replica della definizione di una stored procedure, la replica transazionale consente di replicare l'esecuzione di stored procedure. Ciò risulta utile per la replica dei risultati di stored procedure orientate alla manutenzione che influiscono su ingenti quantità di dati. Per altre informazioni, vedere [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
## <a name="publishing-views"></a>Pubblicazione di viste  
 Tutti i tipi di replica consentono di replicare viste. È possibile copiare la vista e l'indice associato, in caso di vista indicizzata, nel Sottoscrittore, ma è inoltre necessario replicare la tabella di base.  
  
 Per le viste indicizzate, la replica transazionale consente inoltre di replicare la vista indicizzata come tabella anziché come vista, eliminando così l'esigenza di replicare anche la tabella di base. A tale scopo, specificare una delle opzioni "indexed view logbased" per il parametro *\@type* di [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Per altre informazioni sull'uso di **sp_addarticle**, vedere [Definire un articolo](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="publishing-user-defined-functions"></a>Pubblicazione di funzioni definite dall'utente  
 Le istruzioni CREATE FUNCTION per funzioni CLR e [!INCLUDE[tsql](../../../includes/tsql-md.md)] vengono copiate in ogni Sottoscrittore. In caso di funzioni CLR, viene inoltre copiato l'assembly associato. Le modifiche apportate alle funzioni vengono replicate nei Sottoscrittori, mentre non vengono replicate le modifiche agli assembly associati.  
  
## <a name="publishing-user-defined-types-and-alias-data-types"></a>Pubblicazione di tipi di dati definiti dall'utente e tipi di dati alias  
 Le colonne in cui vengono utilizzati tipi definiti dall'utente o tipi di dati alias vengono replicate nei Sottoscrittori come le altre colonne. L'istruzione CREATE TYPE per ogni tipo replicato viene eseguita nel Sottoscrittore prima della creazione della tabella. In caso di tipi definiti dall'utente, viene inoltre copiato l'assembly associato in ogni Sottoscrittore. Le modifiche apportate ai tipi definiti dall'utente e ai tipi di dati alias non vengono replicate nei Sottoscrittori.  
  
 Se a un tipo definito in un database non viene fatto riferimento in alcuna colonna al momento della creazione di una pubblicazione, il tipo non viene copiato nei Sottoscrittori. Se successivamente si crea una colonna di tale tipo nel database e si desidera eseguirne la replica, è innanzitutto necessario copiare manualmente il tipo, nonché l'assembly associato in caso di tipo definito dall'utente, in ogni Sottoscrittore.  
  
## <a name="publishing-full-text-indexes"></a>Pubblicazione di indici full-text  
 L'istruzione CREATE FULLTEXT INDEX viene copiata in ogni Sottoscrittore e nel Sottoscrittore viene creato l'indice full-text. Le modifiche apportate agli indici full-text tramite ALTER FULLTEXT INDEX non vengono replicate.  
  
## <a name="making-schema-changes-to-published-objects"></a>Modifiche dello schema in oggetti pubblicati  
 La replica supporta una vasta gamma di modifiche dello schema negli oggetti pubblicati. Quando si apporta una delle modifiche dello schema seguenti nell'oggetto pubblicato appropriato nel server di pubblicazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , tale modifica viene propagata per impostazione predefinita a tutti i Sottoscrittori [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   MODIFICA TABELLA  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 Per altre informazioni, vedere [Apportare modifiche allo schema nei database di pubblicazione](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="considerations-for-publishing"></a>Considerazioni sulla pubblicazione  
 Durante la pubblicazione di oggetti di database è importante tenere presente quanto segue:  
  
-   Il database è accessibile agli utenti durante la creazione della pubblicazione e dello snapshot iniziale, ma è consigliabile creare le pubblicazioni in periodi di attività ridotta del server di pubblicazione.  
  
-   Non è possibile rinominare un database dopo che vi è stata creata una pubblicazione. Per rinominarlo, è innanzitutto necessario rimuovere la replica dal database.  
  
-   Se si pubblica un oggetto di database che dipende da uno o più oggetti di database diversi, è necessario pubblicare tutti gli oggetti a cui si fa riferimento. Se ad esempio si pubblica una vista che dipende da una tabella, sarà necessario pubblicare anche la tabella.  
  
    > [!NOTE]  
    >  Se in una pubblicazione di tipo merge si aggiunge un nuovo articolo dal quale dipende un articolo esistente, è necessario specificare l'ordine di elaborazione per entrambi gli articoli tramite il parametro **\@processing_order** di [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) e [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Si consideri lo scenario seguente: viene pubblicata una tabella, ma non viene pubblicata una funzione a cui fa riferimento la tabella. Se non si pubblica la funzione, la tabella non può essere creata nel Sottoscrittore. Quando si aggiunge la funzione alla pubblicazione, specificare il valore **1** per il parametro **\@processing_order** di **sp_addmergearticle** e il valore **2** per il parametro **\@processing_order** di **sp_changemergearticle**, indicando il nome della tabella per il parametro **\@article**. Questo ordine di elaborazione consente di creare la funzione nel Sottoscrittore prima della tabella dipendente. È possibile utilizzare numeri diversi per ogni articolo, a condizione che il numero della funzione sia inferiore al numero della tabella.  
  
-   I nomi delle pubblicazioni non possono includere i caratteri seguenti: % * [ ] | : " ? \ / < >.  
  
### <a name="limitations-on-publishing-objects"></a>Limitazioni relative alla pubblicazione di oggetti  
  
-   Il numero massimo di articoli e colonne che è possibile pubblicare varia in base al tipo di pubblicazione. Per altre informazioni, vedere la sezione "Oggetti di replica" in [Specifiche di capacità massima per SQL Server](../../../sql-server/maximum-capacity-specifications-for-sql-server.md).  
  
-   Le stored procedure, le viste, i trigger e le funzioni definite all'utente specificati come WITH ENCRYPTION non possono essere pubblicati nell'ambito della replica [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   È possibile replicare raccolte di XML Schema, ma le modifiche non vengono replicate dopo lo snapshot iniziale.  
  
-   Le tabelle pubblicate per la replica transazionale devono disporre di una chiave primaria. Se una tabella è inclusa in una pubblicazione per la replica transazionale, non è possibile disabilitare gli indici associati a colonne chiave primaria. Questi indici sono necessari per la replica. Per disabilitare un indice, è innanzitutto necessario eliminare la tabella dalla pubblicazione.  
  
-   I valori predefiniti associati creati con [sp_bindefault &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md) non vengono replicati. I valori predefiniti associati sono deprecati e sono stati sostituiti dai valori predefiniti creati con la parola chiave DEFAULT di ALTER TABLE o CREATE TABLE.  
  
-   Le funzioni contenenti l'hint **NOEXPAND** su viste indicizzate non possono essere pubblicate nella stessa pubblicazione delle tabelle con riferimenti e viste indicizzate a causa dell'ordine in cui sono consegnate dall'agente di distribuzione. Per risolvere questo problema, collocare la creazione di tabella e vista indicizzata in una prima pubblicazione, e aggiungere funzioni contenenti l'hint **NOEXPAND** sulle viste indicizzate di una seconda pubblicazione, che sarà pubblicata dopo il completamento della prima. In alternativa, creare script per queste funzioni e recapitare lo script usando il parametro *\@post_snapshot_script* di **sp_addpublication**.  
  
### <a name="schemas-and-object-ownership"></a>Schemi e proprietà degli oggetti  
 In relazione agli schemi e alla proprietà degli oggetti, la replica ha il seguente comportamento predefinito nella Creazione guidata nuova pubblicazione:  
  
-   Per gli articoli di pubblicazioni di tipo merge con un livello di compatibilità 90 o superiore, per le pubblicazioni snapshot e quelle transazionali: per impostazione predefinita, il proprietario dell'oggetto nel Sottoscrittore è uguale al proprietario dell'oggetto corrispondente nel server di pubblicazione. Se nel Sottoscrittore non esistono gli schemi che possiedono gli oggetti, vengono creati automaticamente.  
  
-   Per articoli contenuti in pubblicazioni di tipo merge con un livello di compatibilità inferiore a 90: per impostazione predefinita, il proprietario viene lasciato vuoto e viene specificato come **dbo** durante la creazione dell'oggetto nel Sottoscrittore.  
  
-   Per articoli contenuti in pubblicazioni Oracle: per impostazione predefinita, viene specificato il proprietario **dbo**.  
  
-   Per articoli di pubblicazioni che usano snapshot in modalità carattere (usati per Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e Sottoscrittori [!INCLUDE[ssEW](../../../includes/ssew-md.md)] ): per impostazione predefinita, il proprietario rimane vuoto. Il proprietario viene impostato sul proprietario associato all'account utilizzato dall'agente di distribuzione o dall'agente di merge per la connessione al Sottoscrittore.  
  
 Il proprietario dell'oggetto può essere cambiato tramite la finestra di dialogo **Proprietà articolo - \<**_Article_**>** e tramite le stored procedure **sp_addarticle**, **sp_addmergearticle**, **sp_changearticle** e **sp_changemergearticle**. Per altre informazioni, vedere [Visualizzare e modificare le proprietà della pubblicazione](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), [Definire un articolo](../../../relational-databases/replication/publish/define-an-article.md) e [Visualizzare e modificare le proprietà degli articoli](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
### <a name="publishing-data-to-subscribers-running-previous-versions-of-sql-server"></a>Pubblicazione di dati per Sottoscrittori che eseguono versioni precedenti di SQL Server  
  
-   In caso di pubblicazione per un Sottoscrittore che esegue una versione precedente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è necessario considerare le limitazioni imposte dalle funzionalità di tale versione, sia in termini di funzionalità specifiche della replica che in termini di funzionalità complessive del prodotto.  
  
-   Nelle pubblicazioni di tipo merge viene utilizzato un livello di compatibilità che determina le funzionalità utilizzabili in una pubblicazione e consente di supportare i Sottoscrittori che eseguono versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
### <a name="publishing-tables-in-more-than-one-publication"></a>Pubblicazione di tabelle in più pubblicazioni  
 La replica supporta la pubblicazione di articoli in più pubblicazioni, nonché la ripubblicazione di dati, con le restrizioni seguenti:  
  
-   Se un articolo viene pubblicato in una pubblicazione transazionale o di tipo merge, verificare che la proprietà *\@published_in_tran_pub* sia impostata su TRUE per l'articolo di merge. Per altre informazioni sull'impostazione delle proprietà, vedere [Visualizzare e modificare le proprietà della pubblicazione](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md) e [Visualizzare e modificare le proprietà degli articoli](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
     È anche necessario impostare la proprietà *\@published_in_tran_pub* se un articolo che fa parte di una sottoscrizione transazionale viene incluso in una pubblicazione di tipo merge. In questo caso, è importante tenere presente che, per impostazione predefinita, la replica transazionale prevede che le tabelle nel Sottoscrittore siano considerate di sola lettura. La modifica dei dati di una tabella in una sottoscrizione transazionale durante la replica di tipo merge potrebbe pertanto impedire la convergenza dei dati. Per evitare questa eventualità, è consigliabile specificare queste tabelle come di solo download nella pubblicazione di tipo merge. In tal modo si impedisce al Sottoscrittore di tipo merge di caricare le modifiche ai dati nella tabella. Per altre informazioni, vedere [Ottimizzare le prestazioni della replica di tipo merge con gli articoli di solo download](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
-   Un articolo non può essere pubblicato sia in una pubblicazione di tipo merge che in una pubblicazione transazionale con sottoscrizioni ad aggiornamento in coda.  
  
-   Gli articoli inclusi in pubblicazioni transazionali che supportano le sottoscrizioni aggiornabili non possono essere ripubblicati.  
  
-   Se un articolo viene pubblicato in più pubblicazioni transazionali con supporto delle sottoscrizioni ad aggiornamento in coda, le proprietà seguenti devono contenere lo stesso valore per l'articolo in tutte le pubblicazioni.  
  
    |Proprietà|Parametro di sp_addarticle|  
    |--------------|---------------------------------|  
    |Gestione intervalli di valori Identity|**\@auto_identity_range** (deprecato) e **\@identityrangemangementoption**|  
    |Intervallo di valori Identity del server di pubblicazione|**\@pub_identity_range**|  
    |Intervallo di valori Identity|**\@identity_range**|  
    |Soglia dell'intervallo di valori Identity|**\@threshold**|  
  
     Per altre informazioni su questi parametri, vedere [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
-   Se un articolo viene pubblicato in più pubblicazioni di tipo merge, le proprietà seguenti devono disporre dello stesso valore per l'articolo in tutte le pubblicazioni.  
  
    |Proprietà|Parametro di sp_addmergearticle|  
    |--------------|--------------------------------------|  
    |Rilevamento a livello di colonna|**\@column_tracking**|  
    |Opzioni schema|**\@schema_option**|  
    |Applicazioni filtri alle colonne|**\@vertical_partition**|  
    |Opzioni di caricamento Sottoscrittore|**\@subscriber_upload_options**|  
    |Rilevamento eliminazioni condizionale|**\@delete_tracking**|  
    |Compensazione errori|**\@compensate_for_errors**|  
    |Gestione intervalli di valori Identity|**\@auto_identity_range** (deprecato) e **\@identityrangemangementoption**|  
    |Intervallo di valori Identity del server di pubblicazione|**\@pub_identity_range**|  
    |Intervallo di valori Identity|**\@identity_range**|  
    |Soglia dell'intervallo di valori Identity|**\@threshold**|  
    |Opzioni partizioni|**\@partition_options**|  
    |Flusso colonne BLOB|**\@stream_blob_columns**|  
    |Tipo di filtro|**\@filter_type** (parametro in **sp_addmergefilter**)|  
  
     Per altre informazioni su questi parametri, vedere [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) e [sp_addmergefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md).  
  
-   La replica transazionale e la replica di tipo merge non filtrata supportano la pubblicazione di una tabella in più pubblicazioni e quindi la sottoscrizione all'interno di una singola tabella del database di sottoscrizione, in base allo scenario comunemente denominato di rollup. Il rollup viene frequentemente utilizzato per aggregare subset di dati da più posizioni all'interno di una tabella in un Sottoscrittore centrale. Le pubblicazioni di tipo merge filtrate non supportano lo scenario con Sottoscrittore centrale. Per la replica di tipo merge, il rollup viene in genere implementato tramite una singola pubblicazione con filtri di riga con parametri. Per altre informazioni sui filtri di riga con parametri, vedere [Filtri di riga con parametri](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere ed eliminare articoli in pubblicazioni esistenti](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Configura distribuzione](../../../relational-databases/replication/configure-distribution.md)   
 [Inizializzare una sottoscrizione](../../../relational-databases/replication/initialize-a-subscription.md)   
 [Creazione di script di replica](../../../relational-databases/replication/scripting-replication.md)   
 [Proteggere il server di pubblicazione](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [Sottoscrizione delle pubblicazioni](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
