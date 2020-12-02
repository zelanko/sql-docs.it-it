---
description: Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text
title: Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text
ms.date: 02/02/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], noise words
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 43b5ce7b-9f09-4443-8a5b-c3da6eb28bcc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 54c462ee83fe972eccc9347e8a9f41e570511239
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127758"
---
# <a name="configure-and-manage-stopwords-and-stoplists-for-full-text-search"></a>Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Per garantire l'efficienza di un indice full-text, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è dotato di un meccanismo che rimuove le stringhe più frequenti, inutili ai fini della ricerca. Queste stringhe scartate vengono denominate *parole non significative*. Durante la creazione dell'indice, il motore di ricerca full-text omette le parole non significative dall'indice full-text, in modo che le query full-text non eseguano ricerche in tali parole.  
   
**Parole non significative**. Una parola non significativa può essere una parola con un significato in una lingua specifica. Nella lingua italiana, ad esempio, parole quali "circa", "con", "devo" e "cui" vengono escluse dall'indice full-text poiché in pratica risultano inutili ai fini della ricerca. Una parola non significativa può anche essere un *token* che non ha un significato linguistico.  

**Elenchi di parole non significative**. Le parole non significative vengono gestite nei database utilizzando oggetti denominati elenchi di parole non significative. Un *elenco di parole non significative* è un elenco che, quando associato a un indice full-text, viene applicato alle query full-text su tale indice.
   
## <a name="use-an-existing-stoplist"></a>Usare un elenco di parole non significative esistente  
 È possibile usare un elenco di parole non significative esistente in uno dei modi seguenti:  
  
-   Usare l'elenco di parole non significative fornito dal sistema nel database. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include un elenco di parole non significative che contiene le parole non significative più comuni per ogni lingua supportata, ovvero per ogni lingua associata a word breaker specifici per impostazione predefinita. È possibile copiare l'elenco di parole non significative di sistema e personalizzarne una copia aggiungendone e rimuovendone alcune.  
  
     L'elenco di parole non significative di sistema è installato nel database [Resource](../../relational-databases/databases/resource-database.md) .  
  
-   Usare un elenco di parole non significative personalizzato esistente da qualsiasi altro database nell'istanza del server corrente e quindi aggiungere ed eliminare le parole non significative in base alle specifiche esigenze.  
  
## <a name="create-a-new-stoplist"></a>Creare un nuovo elenco di parole non significative 
### <a name="create-a-new-stoplist-with-transact-sql"></a>Creare un nuovo elenco di parole non significative con Transact-SQL
Usare [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md).

### <a name="create-a-new-stoplist-with-management-studio"></a>Creare un nuovo elenco di parole non significative con Management Studio
  
1.  In Esplora oggetti espandere il server.  
  
2.  Espandere **Database**, quindi espandere il database in cui si vuole creare l'elenco di parole non significative full-text.  
  
3.  Espandere **Archivio**, quindi fare clic con il pulsante destro del mouse su **Elenchi di parole non significative full-text**.  
  
4.  Selezionare **Nuovo elenco di parole non significative full-text**.  
  
5.  Immettere il nome del nuovo elenco.  
  
6.  Facoltativamente, specificare un altro utente come proprietario dell'elenco di parole non significative.  
  
7.  Selezionare una delle opzioni di creazione di un elenco di parole non significative seguenti:  
  
    -   **Creare un elenco di parole non significative vuoto**  
  
    -   **Creare un elenco di parole non significative da un elenco di parole non significative di sistema**  
  
    -   **Creare un elenco di parole non significative da un elenco di parole non significative full-text esistente**  
  
     Per altre informazioni, vedere [Nuovo elenco di parole non significative full-text &#40;pagina Generale&#41;](/previous-versions/sql/sql-server-2016/cc280518(v=sql.130)).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="use-a-stoplist-in-full-text-queries"></a>Usare un elenco di parole non significative nelle query full-text  
 Per usare un elenco di parole non significative nelle query, è necessario associarlo a un indice full-text. È possibile associare un elenco di parole non significative a un indice full-text quando si crea l'indice oppure è possibile modificare l'indice in seguito per aggiungere un elenco.  
  
### <a name="create-a-full-text-index-and-associate-a-stoplist-with-it"></a>Creare un indice full-text e associare un elenco di parole non significative
Usare [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).
  
### <a name="associate-or-disassociate-a-stoplist-with-an-existing-full-text-index"></a>Associare o annullare l'associazione di un elenco di parole non significative a un indice full-text esistente
Usare [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md). 
  
## <a name="change-the-stopwords-in-a-stoplist"></a>Modificare le parole non significative in un elenco  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-transact-sql"></a>Aggiungere o eliminare parole non significative in un elenco con Transact-SQL
Usare [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md).
  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-management-studio"></a>Aggiungere o eliminare parole non significative in un elenco con Management Studio  
  
1.  In Esplora oggetti espandere il server.  
  
2.  Espandere **Database**, quindi espandere il database.  
  
3.  Espandere **Archiviazione**, quindi selezionare **Elenco di parole non significative full-text**.  
  
4.  Fare clic con il pulsante destro del mouse sull'elenco di parole non significative che si vuole modificare, quindi scegliere **Proprietà**.  
  
5.  Nella finestra di dialogo [Proprietà elenco di parole non significative full-text](/previous-versions/sql/sql-server-2016/cc280415(v=sql.130)) :  
  
    1.  Nella casella di riepilogo **Azione** selezionare una delle azioni seguenti: **Aggiungi parola non significativa**, **Elimina parola non significativa**, **Elimina tutte le parole non significative** o **Cancella elenco di parole non significative**.  
  
    2.  Se la casella di testo **Parola non significativa** è abilitata per l'azione selezionata, immettere una singola parola non significativa. Questa parola deve essere univoca, ovvero non ancora inclusa nell'elenco di parole non significative per la lingua selezionata.  
  
    3.  Se la casella di riepilogo **Full-text language** è abilitata per l'azione selezionata, selezionare una lingua.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="manage-stoplists-and-their-usage"></a>Gestire gli elenchi di parole non significative e il relativo utilizzo
  
### <a name="view-all-the-stopwords-in-a-stoplist"></a>Visualizzare tutte le parole non significative riunite in un elenco
Usare [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md). 
  
### <a name="get-info-about-all-the-stoplists-in-the-current-database"></a>Ottenere informazioni su tutti gli elenchi di parole non significative nel database corrente
Usare [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md) e [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md).
  
### <a name="view-the-tokenization-result-of-a-word-breaker-thesaurus-and-stoplist-combination"></a>Visualizzare il risultato della suddivisione in token di una combinazione di word breaker, thesaurus ed elenchi di parole non significative
Usare [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md).

### <a name="suppress-an-error-message-if-stopwords-cause-a-boolean-operation-on-a-full-text-query-to-fail"></a>Eliminare un messaggio di errore visualizzato nel caso in cui le parole non significative impediscono l'esecuzione di un'operazione booleana in una query full-text
Usare l'[opzione di configurazione del server transform noise words](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md). 
   
## <a name="more-info-about-stopword-position"></a>Altre informazioni sulla posizione delle parole non significative
 Anche se ignora l'inclusione di parole non significative, l'indice full-text ne prende in considerazione la posizione. Si consideri ad esempio la frase "Istruzioni non valide per questi modelli Adventure Works Cycles". Nella tabella seguente viene illustrata la posizione delle parole nella frase:  
  
|Word|Posizione|  
|----------|--------------|  
|Istruzioni|1|  
|non|2|  
|valide|3|  
|su|4|  
|questi|5|  
|modelli|6|  
|Adventure|7|  
|Cicli|8|  
|modelli|9|  
  
 Le parole non significative "sono", "in" e "questi" nelle posizioni 2, 4 e 5 vengono escluse dall'indice full-text. Le relative informazioni di posizione vengono comunque mantenute, lasciando invariata la posizione delle altre parole nella frase.   
  
## <a name="upgrade-noise-words-from-sql-server-2005"></a>Aggiornare le parole non significative da SQL Server 2005  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Le parole non significative di  sono state sostituite. Quando si aggiorna un database da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], i file delle parole non significative non vengono più utilizzati. Tali file vengono tuttavia archiviati nella cartella FTDATA\ FTNoiseThesaurusBak e possono essere utilizzati in seguito durante l'aggiornamento o la compilazione di elenchi di parole non significative corrispondenti. Per informazioni sull'aggiornamento dei file delle parole non significative agli elenchi corrispondenti, vedere [Aggiornamento della ricerca full-text](../../relational-databases/search/upgrade-full-text-search.md).  
  
  
