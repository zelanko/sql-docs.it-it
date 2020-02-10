---
title: Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fe48b26960db591ce803b1f110e9293fd22d6554
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011519"
---
# <a name="configure-and-manage-stopwords-and-stoplists-for-full-text-search"></a>Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text
  Per garantire l'efficienza di un indice full-text, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è dotato di un meccanismo che rimuove le stringhe più frequenti, inutili ai fini della ricerca. Queste stringhe scartate vengono denominate *parole non significative*. Durante la creazione dell'indice, il motore di ricerca full-text omette le parole non significative dall'indice full-text, in modo che le query full-text non eseguano ricerche in tali parole.  
  
##  <a name="understand"></a>Informazioni su parole non significative e elenchi  
 Una parola non significativa può essere una parola con un significato in un linguaggio specifico o può essere un *token* che non dispone di significato linguistico. Nella lingua italiana, ad esempio, parole quali "circa", "con", "devo" e "cui" vengono escluse dall'indice full-text poiché in pratica risultano inutili ai fini della ricerca.  
  
 Anche se ignora l'inclusione di parole non significative, l'indice full-text ne prende in considerazione la posizione. Si consideri ad esempio la frase "Istruzioni non valide per questi modelli Adventure Works Cycles". Nella tabella seguente viene illustrata la posizione delle parole nella frase:  
  
|Word|Posizione|  
|----------|--------------|  
|Istruzioni|1|  
|non|2|  
|valide|3|  
|to|4|  
|questi|5|  
|modelli|6|  
|Adventure|7|  
|Cicli|8|  
|modelli|9|  
  
 Le parole non significative "sono", "in" e "questi" nelle posizioni 2, 4 e 5 vengono escluse dall'indice full-text. Le relative informazioni di posizione vengono comunque mantenute, lasciando invariata la posizione delle altre parole nella frase.  
  
 Le parole non significative vengono gestite nei database utilizzando oggetti denominati elenchi di parole non significative. Un *elenco di parole non significative* è un elenco che, quando associato a un indice full-text, viene applicato alle query full-text su tale indice.  
  
  
##  <a name="creating"></a>Creazione di un oggetto di parole non significative  
 È possibile creare un elenco di parole non significative in uno dei modi seguenti:  
  
-   Utilizzando l'elenco di parole non significative fornito dal sistema nel database. L'elenco di parole non significative di sistema incluso in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene le parole non significative più comuni per ogni lingua supportata, ovvero per ogni lingua associata a word breaker specifici per impostazione predefinita. L'elenco di parole non significative contiene le parole non significative comuni per tutte le lingue supportate.  È possibile copiare l'elenco di parole non significative di sistema e personalizzarne una copia aggiungendone e rimuovendone alcune.  
  
     L'elenco di parole non significative di sistema è installato nel database [Resource](../databases/resource-database.md) .  
  
-   Creando un elenco di parole non significative personalizzato, quindi aggiungendovi altre parole non significative per ogni lingua specificata. Se necessario, è inoltre possibile eliminare parole non significative dall'elenco.  
  
-   Utilizzando un elenco di parole non significative personalizzato esistente da qualsiasi altro database nell'instanza del server corrente e successivamente aggiungendo ed eliminando le parole non significative in base alle specifiche esigenze.  
  
 **Per creare un elenco di parole non significative**  
  
-   [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)  
  
#### <a name="to-create-a-full-text-stoplist-in-management-studio"></a>Per creare un elenco di parole non significative full-text in Management Studio  
  
1.  In Esplora oggetti espandere il server.  
  
2.  Espandere **Database**, quindi espandere il database in cui si vuole creare l'elenco di parole non significative full-text.  
  
3.  Espandere **Archivio**, quindi fare clic con il pulsante destro del mouse su **Elenchi di parole non significative full-text**.  
  
4.  Selezionare **Nuovo elenco di parole non significative full-text**.  
  
5.  Specificare il nome dell'elenco di parole non significative.  
  
6.  Facoltativamente, specificare un altro utente come proprietario dell'elenco di parole non significative.  
  
7.  Selezionare una delle opzioni di creazione di un elenco di parole non significative seguenti:  
  
    -   **Creare un elenco di parole non significative vuoto**  
  
    -   **Creare un elenco di parole non significative da un elenco di parole non significative di sistema**  
  
    -   **Creare un elenco di parole non significative da un elenco di parole non significative full-text esistente**  
  
     Per altre informazioni, vedere [Nuovo elenco di parole non significative full-text &#40;pagina Generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md).  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 **Per eliminare un elenco di parole non significative**  
  
-   [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  
##  <a name="queries"></a>Utilizzo di un oggetto di parole non significative nelle query full-text  
 Per utilizzare un elenco di parole non significative nelle query, è necessario associarlo a un indice full-text. È possibile associare un elenco di parole non significative a un indice full-text quando si crea l'indice oppure è possibile modificare l'indice in seguito per aggiungere un elenco.  
  
 **Per creare un indice full-text e associare un elenco di parole non significative**  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
 **Per associare o annullare l'associazione di un elenco di parole non significative a un indice full-text esistente**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
 **Per eliminare un messaggio di errore visualizzato nel caso in cui le parole non significative impediscono l'esecuzione di un'operazione booleana in una query full-text**  
  
-   [Opzione di configurazione del server transform noise words Server](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)  
  
  
##  <a name="viewing"></a>Visualizzazione dei metadati di elenchi e di parole non significative  
 **Per visualizzare tutte le parole non significative di un elenco**  
  
-   [sys.fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)  
  
 **Per ottenere informazioni su tutti gli elenchi di parole non significative nel database corrente**  
  
-   [sys.fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)  
  
-   [sys.fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)  
  
 **Per visualizzare il risultato della suddivisione in token di una combinazione di word breaker, thesaurus ed elenchi di parole non significative**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)  
  
  
##  <a name="change"></a>Modifica di parole non significative in un oggetto di parole non significative  
 **Per aggiungere o eliminare parole non significative in un elenco**  
  
-   [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)  
  
#### <a name="to-change-the-stopwords-in-a-stoplist-in-management-studio"></a>Per modificare le parole non significative in un elenco di parole non significative in Management Studio  
  
1.  In Esplora oggetti espandere il server.  
  
2.  Espandere **Database**, quindi espandere il database.  
  
3.  Espandere **Archiviazione**, quindi selezionare **Elenco di parole non significative full-text**.  
  
4.  Fare clic con il pulsante destro del mouse sull'elenco di parole non significative che si vuole modificare, quindi scegliere **Proprietà**.  
  
5.  Nella finestra di dialogo [Proprietà elenco di parole non significative full-text](../../database-engine/full-text-stoplist-properties.md) :  
  
    1.  Nella casella di riepilogo **Azione** selezionare una delle azioni seguenti: **Aggiungi parola non significativa**, **Elimina parola non significativa**, **Elimina tutte le parole non significative**o **Cancella elenco di parole non significative**.  
  
    2.  Se la casella di testo **Parola non significativa** è abilitata per l'azione selezionata, immettere una singola parola non significativa. Questa parola deve essere univoca, ovvero non ancora inclusa nell'elenco di parole non significative per la lingua selezionata.  
  
    3.  Se la casella di riepilogo **Full-text language** è abilitata per l'azione selezionata, selezionare una lingua.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
##  <a name="upgrade"></a>Aggiornamento delle parole non significative da SQL Server 2005  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Le parole non significative di  sono state sostituite. Quando si aggiorna un database da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], i file delle parole non significative non vengono più utilizzati. Tali file vengono tuttavia archiviati nella cartella FTDATA\ FTNoiseThesaurusBak e possono essere utilizzati in seguito durante l'aggiornamento o la compilazione di elenchi di parole non significative corrispondenti. Per informazioni sull'aggiornamento dei file delle parole non significative agli elenchi corrispondenti, vedere [Aggiornamento della ricerca full-text](upgrade-full-text-search.md).  
  
  
  
