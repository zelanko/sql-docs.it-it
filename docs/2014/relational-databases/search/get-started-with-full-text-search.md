---
title: Introduzione alla ricerca full-text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b6dc03709ea16fb718ff93ed60f75ad4d1515eaf
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541392"
---
# <a name="get-started-with-full-text-search"></a>Introduzione alla ricerca full-text
  Per impostazione predefinita, nei database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è abilitata la funzionalità full-text. Per utilizzare un indice full-text in una tabella, è tuttavia necessario impostare la funzionalità di indicizzazione full-text nelle colonne delle tabelle a cui si desidera accedere mediante il motore di ricerca full-text.  
  
##  <a name="configure"></a> Configurazione di un Database per la ricerca Full-Text  
 Per qualsiasi scenario, un amministratore di database esegue i passaggi di base seguenti per configurare le colonne di tabella di un database per la ricerca full-text:  
  
1.  Creazione di un catalogo full-text.  
  
2.  In ogni tabella in cui eseguire la ricerca è necessario creare un indice full-text.  
  
    1.  Identificare ogni colonna di testo che si desidera includere nell'indice full-text.  
  
    2.  Se una determinata colonna contiene documenti archiviati come dati binari (`varbinary(max)`, o `image` dei dati), è necessario specificare una colonna di tabella (la *colonna di tipo*) che identifica il tipo di ogni documento nella colonna da indicizzare.  
  
    3.  Specificare la lingua che verrà utilizzata dalla ricerca full-text nei documenti nella colonna.  
  
    4.  Scegliere il meccanismo di rilevamento delle modifiche che si desidera utilizzare per l'indice full-text per rilevare le modifiche nella tabella di base e nelle relative colonne.  
  
 La ricerca full-text supporta più lingue con l'uso dei *componenti linguistici* seguenti: word breaker e stemmer, elenchi di parole non significative e file del thesaurus. I file del thesaurus e, in alcuni casi, gli elenchi di parole non significative richiedono la configurazione da parte di un amministratore di database. Un determinato file del thesaurus supporta tutti gli indici full-text che utilizzano la lingua corrispondente. È inoltre possibile associare un determinato elenco di parole non significative al numero desiderato di indici full-text.  
  
##  <a name="setup"></a> Impostazione di un catalogo Full-Text e un indice  
 L'operazione comporta i passaggi principali seguenti:  
  
1.  Creazione di un catalogo full-text per archiviare indici full-text.  
  
     Ogni indice full-text deve appartenere a un catalogo full-text. È possibile creare un catalogo di testo separato per ogni indice full-text oppure associare più indici full-text a un determinato catalogo. Un catalogo full-text è un oggetto virtuale e non appartiene ad alcun filegroup. Il catalogo full-text è un concetto logico che fa riferimento a un gruppo di indici full-text.  
  
2.  Creazione di un indice full-text nella tabella o vista indicizzata.  
  
     Un indice full-text è un tipo speciale di indice funzionale basato su token compilato e gestito dal motore di ricerca full-text. Per creare una ricerca full-text su una tabella o una vista, è necessario disporre di un indice univoco a colonna singola che non ammette valori Null. Questo indice univoco viene utilizzato dal motore di ricerca full-text per eseguire il mapping di ogni riga della tabella a una chiave univoca comprimibile. Un indice full-text può includere colonne `char`, `varchar`, `nchar`, `nvarchar`, `text`, `ntext`, `image`, `xml`, `varbinary` e `varbinary(max)`. Per altre informazioni, vedere [Creare e gestire indici full-text](create-and-manage-full-text-indexes.md).  
  
 Prima di imparare a creare indici full-text, è importante valutare le differenze rispetto ai normali indici [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nella tabella seguente vengono elencate tali differenze.  
  
|Indici full-text|Indici di SQL Server normali|  
|------------------------|--------------------------------|  
|È consentito un solo indice full-text per tabella.|Sono consentiti più indici normali per tabella.|  
|L'aggiunta di dati a indici full-text, definita *popolamento*, può essere richiesta in modo specifico, tramite pianificazione oppure può avvenire in modo automatico con l'aggiunta di nuovi dati.|Vengono automaticamente aggiornati quando si inseriscono, aggiornano o eliminano dati.|  
|Sono raggruppati all'interno dello stesso database in uno o più cataloghi full-text.|Non sono raggruppati.|  
  
  
##  <a name="options"></a> Scelta di opzioni per un indice Full-Text  
 In questa sezione vengono trattati i seguenti argomenti:  
  
-   Scelta della lingua delle colonne  
  
-   Scelta di un filegroup per un indice full-text  
  
-   Assegnazione dell'indice full-text a un catalogo full-text  
  
-   Associazione di un elenco di parole non significative all'indice full-text  
  
-   Aggiornamento di un indice full-text  
  
### <a name="choosing-the-column-language"></a>Scelta della lingua delle colonne  
 Per informazioni sugli aspetti da considerare nella scelta della lingua delle colonne, vedere [Scelta di una lingua durante la creazione di un indice full-text](choose-a-language-when-creating-a-full-text-index.md).  
  
### <a name="choosing-a-filegroup-for-a-full-text-index"></a>Scelta di un filegroup per un indice full-text  
 Il processo di compilazione di un indice full-text richiede l'esecuzione di molte operazioni di I/O (in senso lato, consiste nella lettura di dati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e nella propagazione dei dati filtrati all'indice full-text). La procedura consigliata consiste nell'individuare l'indice full-text nel filegroup del database ideale per ottimizzare le prestazioni di I/O oppure gli indici full-text in un filegroup diverso in un altro volume.  
  
 Per semplificare la gestione, è consigliabile archiviare i dati delle tabelle ed eventuali cataloghi full-text associati nello stesso filegroup. Per motivi legati alle prestazioni, potrebbe essere necessario mantenere i dati delle tabelle e l'indice full-text in filegroup diversi archiviati in volumi diversi allo scopo di ottimizzare il parallelismo di I/O.  
  
  
### <a name="assigning-the-full-text-index-to-a-full-text-catalog"></a>Assegnazione dell'indice full-text a un catalogo full-text  
 È importante pianificare la posizione di indici full-text per le tabelle in cataloghi full-text.  
  
 È consigliabile associare nello stesso catalogo full-text le tabelle con caratteristiche di aggiornamento equivalenti, ad esempio un numero ridotto o elevato di modifiche oppure modifiche frequenti apportate a una determinata ora del giorno. Pianificando il popolamento del catalogo full-text, gli indici full-text mantengono la sincronizzazione con le tabelle senza influire negativamente sull'utilizzo delle risorse del server di database durante i periodi di elevata attività del database.  
  
 Quando si assegna una tabella a un catalogo full-text, considerare le linee guida seguenti:  
  
-   Selezionare sempre il più piccolo indice univoco disponibile per la chiave univoca full-text. Un indice basato su valori interi a quattro byte è l'impostazione ottimale. Ciò consente di ridurre notevolmente le risorse richieste dal servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search nel file system. Se la chiave primaria è di grandi dimensioni (oltre 100 byte), considerare la possibilità di scegliere un altro indice univoco nella tabella (o di creare un altro indice univoco) come chiave univoca full-text. In caso contrario, se le dimensioni della chiave univoca raggiungono il massimo consentito (900 byte), non sarà possibile eseguire il popolamento full-text.  
  
-   Se viene indicizzata una tabella che include milioni di righe, assegnarla al proprio catalogo full-text.  
  
-   Considerare la quantità di modifiche apportate alle tabelle durante l'indicizzazione full-text, nonché il numero totale di righe. Se il numero totale di righe modificate sommato al numero di righe della tabella presenti durante l'ultimo popolamento full-text corrisponde a milioni di righe, assegnare la tabella al proprio catalogo full-text.  
  
  
### <a name="associating-a-stoplist-with-the-full-text-index"></a>Associazione di un elenco di parole non significative all'indice full-text  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] sono stati introdotti gli elenchi di parole non significative. Un *elenco di parole non significative* è un elenco di termini che non vengono considerati nelle query, viene associato a ogni indice full-text e le parole in esso contenute vengono applicate alle query full-text di quell'indice. Per impostazione predefinita, a un nuovo indice full-text viene associato l'elenco di parole non significative di sistema. È tuttavia possibile creare e utilizzare un elenco di parole non significative personalizzato. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 Ad esempio, l'istruzione [CREATE FULLTEXT STOPLIST](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] seguente consente di creare un nuovo elenco di parole non significative full-text denominato myStoplist3, copiando dall'elenco di parole non significative di sistema:  
  
```  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 L'istruzione [ALTER FULLTEXT STOPLIST](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] seguente consente di modificare un elenco di parole non significative denominato myStoplist, aggiungendo la parola "en" per lo spagnolo e poi per il francese:  
  
```  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
  
  
### <a name="updating-a-full-text-index"></a>Aggiornamento di un indice full-text  
 Come i normali indici [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], gli indici full-text possono essere aggiornati automaticamente alla modifica dei dati delle tabelle associate. Questo è il comportamento predefinito. In alternativa, è possibile aggiornare gli indici full-text manualmente o a intervalli pianificati specificati. Poiché il popolamento di un indice full-text può richiedere tempi lunghi e l'utilizzo di molte risorse, l'aggiornamento dell'indice full-text viene in genere eseguito in background come processo asincrono in seguito alle modifiche apportate alla tabella di base. L'aggiornamento immediato di un indice full-text dopo ogni modifica apportata alla tabella di base può richiedere l'utilizzo di molte risorse. Pertanto, se la frequenza con cui si eseguono aggiornamenti, inserimenti ed eliminazioni è molto elevata, è possibile notare un calo delle prestazioni a livello di esecuzione delle query. In questo caso, considerare la pianificazione di aggiornamenti con rilevamento manuale delle modifiche per gestire gradualmente le numerose modifiche, anziché dividere le risorse con le query.  
  
 Per monitorare lo stato del popolamento, utilizzare la funzione FULLTEXTCATALOGPROPERTY o OBJECTPROPERTYEX. Per ottenere lo stato del popolamento del catalogo, eseguire l'istruzione seguente:  
  
```  
SELECT FULLTEXTCATALOGPROPERTY('AdvWksDocFTCat', 'Populatestatus');  
```  
  
 In genere, se è in corso un popolamento completo, il risultato restituito è 1.  
  
  
##  <a name="example"></a> Esempio: Impostazione della ricerca Full-Text  
 L'esempio in due parti seguente consiste nella creazione di un catalogo full-text denominato `AdvWksDocFTCat` nel database AdventureWorks e quindi nella creazione di un indice full-text nella tabella `Document` in [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Questa istruzione determina la creazione del catalogo full-text nella directory predefinita specificata durante l'installazione. La cartella denominata `AdvWksDocFTCat` si trova nella directory predefinita.  
  
1.  Per creare un catalogo full-text denominato `AdvWksDocFTCat`, nell'esempio viene usata un'istruzione [CREATE FULLTEXT CATALOG](/sql/t-sql/statements/create-fulltext-catalog-transact-sql):  
  
    ```  
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
  
2.  Prima di creare un indice full-text nella tabella Document, assicurarsi che la tabella disponga di un indice univoco a singola colonna che non ammette valori Null. L'istruzione [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) seguente consente di creare un indice univoco, `ui_ukDoc`, nella colonna DocumentID della tabella Document:  
  
    ```  
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  
  
3.  Quando si dispone di una chiave univoca, è possibile creare un indice full-text nella tabella `Document` usando l'istruzione [CREATE FULLTEXT INDEX](/sql/t-sql/statements/create-fulltext-index-transact-sql) seguente.  
  
    ```  
    CREATE FULLTEXT INDEX ON Production.Document  
    (  
        Document                         --Full-text index column name   
            TYPE COLUMN FileExtension    --Name of column that contains file type information  
            Language 2057                 --2057 is the LCID for British English  
    )  
    KEY INDEX ui_ukDoc ON AdvWksDocFTCat --Unique index  
    WITH CHANGE_TRACKING AUTO            --Population type;  
    GO  
  
    ```  
  
     L'elemento TYPE COLUMN definito in questo esempio specifica la colonna del tipo nella tabella che contiene il tipo di documento in ciascuna riga della colonna 'Document' (che è di tipo binario). La colonna di tipo archivia i file fornita dall'utente estensione-"doc", "xls" e così via del documento in una determinata riga. Il motore di ricerca full-text utilizza l'estensione file in una determinata riga per richiamare il filtro corretto da utilizzare per l'analisi dei dati di quella riga. Al termine dell'analisi dei dati binari della riga eseguita tramite il filtro, il word breaker specificato analizzerà il contenuto. In questo esempio viene utilizzato il word breaker per l'Inglese britannico. Si noti che il processo di filtro viene eseguito unicamente durante l'indicizzazione o quando un utente inserisce o aggiorna una colonna della tabella di base con il rilevamento delle modifiche automatico abilitato per l'indice full-text. Per altre informazioni, vedere [Configurazione e gestione di filtri per la ricerca](configure-and-manage-filters-for-search.md).  
  
  
##  <a name="tasks"></a> Attività comuni  
  
### <a name="to-create-a-full-text-catalog"></a>Per creare un catalogo full-text  
  
-   [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)  
  
-   [Creare e gestire cataloghi full-text](create-and-manage-full-text-catalogs.md)  
  
### <a name="to-view-the-indexes-of-a-table-or-view"></a>Per visualizzare gli indici di una tabella (o vista)  
  
-   [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)  
  
### <a name="to-create-a-unique-index"></a>Per creare un indice univoco  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
-   [Aprire Progettazione tabelle &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)  
  
### <a name="to-create-a-full-text-index"></a>Per creare un indice full-text  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
-   [Creazione e gestione di indici full-text](create-and-manage-full-text-indexes.md)  
  
### <a name="to-view-information-about-a-full-text-index"></a>Per visualizzare informazioni su un indice full-text  
  
|Catalogo o vista a gestione dinamica|Descrizione|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql)|Restituisce una riga per ogni catalogo full-text in riferimento all'indice full-text.|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|Contiene una riga per ogni colonna che fa parte di un indice full-text.|  
|[sys.fulltext_index_fragments &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql)|Un indice full-text utilizza tabelle interne denominate frammenti di indice full-text per archiviare i dati dell'indice invertito. Questa vista può essere utilizzata per eseguire una query sui metadati relativi a tali frammenti. Nella vista è contenuta una riga per ogni frammento di indice full-text presente in ogni tabella contenente un indice full-text.|  
|[sys.fulltext_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql)|Contiene una riga per indice full-text di un oggetto in formato di tabella.|  
|[sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql)|Restituisce informazioni sul contenuto di un indice full-text per la tabella specificata.|  
|[sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql)|Restituisce informazioni sul contenuto a livello di documento di un indice full-text per la tabella specificata. Una determinata parola chiave può essere inclusa in diversi documenti.|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|Restituisce informazioni sui popolamenti di indici full-text in corso.|  
  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [Popolamento degli indici full-text](populate-full-text-indexes.md)   
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)  
  
  
