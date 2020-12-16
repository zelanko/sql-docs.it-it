---
description: Introduzione alla ricerca full-text
title: Introduzione alla ricerca full-text | Microsoft Docs
ms.date: 03/31/2020
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ffb6aefd828d9e329df6b624669f7d025d6044f7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479522"
---
# <a name="get-started-with-full-text-search"></a>Introduzione alla ricerca full-text
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
La funzionalità full-text è abilitata per impostazione predefinita nei database di SQL Server. Prima di poter eseguire query full-text, è necessario creare un catalogo full-text completo e un indice full-text nelle tabelle o nelle viste indicizzate in cui si vuole eseguire la ricerca.

## <a name="set-up-full-text-search-in-two-steps"></a>Configurare la ricerca full-text in due passaggi
Per configurare la ricerca full-text sono richiesti due passaggi di base:  
1.  Creazione di un catalogo full-text.  
2.  Creare un indice full-text nelle tabelle o nelle viste indicizzate in cui eseguire la ricerca. 

Ogni indice full-text deve appartenere a un catalogo full-text. È possibile creare un catalogo di testo separato per ogni indice full-text oppure associare più indici full-text a un determinato catalogo. Un catalogo full-text è un oggetto virtuale e non appartiene ad alcun filegroup. Il catalogo full-text è un concetto logico che fa riferimento a un gruppo di indici full-text.

> [!NOTE]
> Questa procedura presuppone che siano stati installati i componenti facoltativi della ricerca full-text durante l'installazione di SQL Server. In caso contrario, è necessario eseguire di nuovo il programma di installazione di SQL Server per aggiungerli.  

## <a name="set-up-full-text-search-with-a-wizard"></a>Configurare la ricerca full-text con una procedura guidata 
 
Per configurare la ricerca full-text con una procedura guidata, vedere [Usare l'Indicizzazione guidata full-text](../../relational-databases/search/use-the-full-text-indexing-wizard.md).

## <a name="set-up-full-text-search-with-transact-sql"></a>Configurare la ricerca full-text con Transact-SQL 
 L'esempio in due parti seguente consiste nella creazione di un catalogo full-text denominato `AdvWksDocFTCat` nel database di esempio AdventureWorks e quindi nella creazione di un indice full-text nella tabella `Document` nel database di esempio. Questa istruzione crea il catalogo full-text nella directory predefinita specificata durante l'installazione di SQL Server. La cartella denominata `AdvWksDocFTCat` si trova nella directory predefinita.  
  
1.  Per creare un catalogo full-text denominato `AdvWksDocFTCat`, nell'esempio viene usata un'istruzione [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md) :  
  
    ```sql
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
    Per altre informazioni, vedere [Creare e gestire cataloghi full-text](../../relational-databases/search/create-and-manage-full-text-catalogs.md).
 
2.  Prima di creare un indice full-text nella tabella Document, assicurarsi che la tabella disponga di un indice univoco a singola colonna che non ammette valori Null. L'istruzione [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) seguente consente di creare un indice univoco, `ui_ukDoc`, nella colonna DocumentID della tabella Document:  
  
    ```sql 
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentNode);  
    ```  

3.  Eliminare l'indice full-text esistente nella tabella `Document` usando l'istruzione [DROP FULLTEXT INDEX](../../t-sql/statements/drop-fulltext-index-transact-sql.md) seguente. 

    ```sql
    DROP FULLTEXT INDEX ON Production.Document
    GO
    ```

4.  Quando si dispone di una chiave univoca, è possibile creare un indice full-text nella tabella `Document` usando l'istruzione [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) seguente.  
  
    ```sql  
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
    
  
  
     L'elemento TYPE COLUMN definito in questo esempio specifica la colonna del tipo nella tabella che contiene il tipo di documento in ciascuna riga della colonna 'Document' (che è di tipo binario). Nella colonna del tipo è archiviata l'estensione di file fornita dall'utente, ovvero "doc", "xls" e così via, del documento in una determinata riga. Il motore di ricerca full-text utilizza l'estensione file in una determinata riga per richiamare il filtro corretto da utilizzare per l'analisi dei dati di quella riga. Al termine dell'analisi dei dati binari della riga eseguita tramite il filtro, il word breaker specificato analizzerà il contenuto. In questo esempio viene usato il word breaker per l'Inglese britannico. Per altre informazioni, vedere [Configurazione e gestione di filtri per la ricerca](../../relational-databases/search/configure-and-manage-filters-for-search.md).  

    Per altre informazioni, vedere [Creare e gestire indici full-text](../../relational-databases/search/create-and-manage-full-text-indexes.md).

##  <a name="choose-options-for-a-full-text-index"></a><a name="options"></a> Scegliere le opzioni per un indice full-text 
  
### <a name="choose-a-language"></a>Scegliere una lingua  
 Per informazioni sulla scelta della lingua delle colonne, vedere [Scegliere una lingua durante la creazione di un indice full-text](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
### <a name="choose-a-filegroup"></a>Scegliere un filegroup  
 Il processo di compilazione di un indice full-text richiede l'esecuzione di molte operazioni di I/O. In sintesi, consiste nella lettura di dati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi nella propagazione dei dati filtrati all'indice full-text. La procedura consigliata consiste nell'individuare l'indice full-text nel filegroup del database ideale per ottimizzare le prestazioni di I/O oppure gli indici full-text in un filegroup diverso in un altro volume.
  
### <a name="choose-a-full-text-catalog"></a>Scegliere un catalogo full-text   
 
 È consigliabile associare nello stesso catalogo full-text le tabelle con caratteristiche di aggiornamento equivalenti, ad esempio un numero ridotto o elevato di modifiche oppure modifiche frequenti apportate a una determinata ora del giorno. Pianificando il popolamento del catalogo full-text, gli indici full-text mantengono la sincronizzazione con le tabelle senza influire negativamente sull'utilizzo delle risorse del server di database durante i periodi di elevata attività del database.  
  
 Considerare le linee guida seguenti:  
  
-   Se viene indicizzata una tabella che include milioni di righe, assegnarla al relativo catalogo full-text.  
  
-   Considerare la quantità di modifiche apportate alle tabelle durante l'indicizzazione full-text, nonché il numero totale di righe. Se il numero totale di righe modificate sommato al numero di righe della tabella presenti durante l'ultimo popolamento full-text corrisponde a milioni di righe, assegnare la tabella al relativo catalogo full-text.  

### <a name="associate-a-unique-index"></a>Associare un indice univoco
Selezionare sempre il più piccolo indice univoco disponibile per la chiave univoca full-text. Un indice basato su valori interi a quattro byte è l'impostazione ottimale. Ciò consente di ridurre notevolmente le risorse richieste dal servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search nel file system. Se la chiave primaria è di grandi dimensioni (oltre 100 byte), considerare la possibilità di scegliere un altro indice univoco nella tabella (o di creare un altro indice univoco) come chiave univoca full-text. In caso contrario, se le dimensioni della chiave univoca raggiungono il massimo consentito (900 byte), non sarà possibile eseguire il popolamento full-text.  
 
### <a name="associate-a-stoplist"></a>Associare un elenco di parole non significative   
  Un *elenco di parole non significative* è un elenco di termini che non vengono considerati nelle query, viene associato a ogni indice full-text e le parole in esso contenute vengono applicate alle query full-text di quell'indice. Per impostazione predefinita, a un nuovo indice full-text viene associato l'elenco di parole non significative di sistema. È anche possibile creare e usare un elenco di parole non significative personalizzato.   
  
 Ad esempio, l'istruzione [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md) di [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente consente di creare un nuovo elenco di parole non significative full-text denominato myStoplist, copiando dall'elenco di parole non significative di sistema:  
  
```sql  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 L'istruzione [ALTER FULLTEXT STOPLIST](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md) di [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente consente di modificare un elenco di parole non significative denominato myStoplist, aggiungendo la parola "en" per lo spagnolo e poi per il francese:  
  
```sql  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).

## <a name="update-a-full-text-index"></a>Aggiornare un indice full-text  
 Come i normali indici [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , gli indici full-text possono essere aggiornati automaticamente alla modifica dei dati delle tabelle associate. Questo è il comportamento predefinito. In alternativa, è possibile aggiornare gli indici full-text manualmente o a intervalli pianificati specificati. Il popolamento di un indice full-text può richiedere molto tempo e risorse. L'aggiornamento dell'indice full-text viene pertanto eseguito di solito in background come processo asincrono in seguito alle modifiche apportate alla tabella di base. 
 
Anche l'aggiornamento immediato di un indice full-text dopo ogni modifica apportata alla tabella di base può richiedere l'uso di molte risorse. Pertanto, se la frequenza con cui si eseguono aggiornamenti, inserimenti ed eliminazioni è elevata, è possibile notare un calo delle prestazioni delle query. In questo caso, considerare la pianificazione di aggiornamenti con rilevamento manuale delle modifiche per gestire gradualmente le numerose modifiche, anziché dividere le risorse con le query.  
  
Per altre informazioni, vedere [Popolare gli indici full-text](../../relational-databases/search/populate-full-text-indexes.md). 

## <a name="next-steps"></a>Passaggi successivi
Dopo aver configurato la ricerca full-text di SQL Server, si è pronti per eseguire query full-text. Per altre informazioni, vedere [Eseguire query con ricerca full-text](../../relational-databases/search/query-with-full-text-search.md).
