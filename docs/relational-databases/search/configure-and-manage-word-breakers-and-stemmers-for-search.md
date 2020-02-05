---
title: Configurare e gestire word breaker e stemmer per la ricerca
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- full-text search [SQL Server], stemmers
- linguistic analysis [full-text search]
- full-text indexes [SQL Server], linguistic analysis
- full-text search [SQL Server], word breakers
- default full-text language option
- stemmers [full-text search]
- conjugating verbs [full-text search]
- word breakers [full-text search]
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 393b6e248962fa496dcdac9fe5def556b766a2bd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74056266"
---
# <a name="configure--manage-word-breakers--stemmers-for-search-sql-server"></a>Configurare e gestire word breaker e stemmer per la ricerca (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Word breaker e stemmer eseguono l'analisi linguistica su tutti i dati con indicizzazione full-text. L'analisi linguistica esegue le due operazioni seguenti:

-   **Trovare i delimitatori di parola (word breaking)** . Lo *word breaker* identifica singole parole determinando i delimitatori di parola in base alle regole lessicali della lingua. Ogni parola ( *token*) viene inserita nell'indice full-text utilizzando una rappresentazione compressa per ridurre le relative dimensioni.

-   **Coniugare i verbi (stemming)** . Lo *stemmer* genera forme flessive di una particolare parola in base alle regole di quella lingua, ad esempio "running", "ran" e "runner" sono varie forme della parola "run".

## <a name="word-breakers-and-stemmers-are-language-specific"></a>I word breaker e gli stemmer sono specifici della lingua

Word breaker e stemmer sono specifici della lingua e le regole per l'analisi linguistica variano a seconda della lingua. L'uso di word breaker specifici di ogni lingua consente una maggiore accuratezza dei termini risultanti per le diverse lingue.

Per usare word breaker e stemmer forniti per tutte le lingue supportate da SQL Server, in genere non è necessario intraprendere alcuna azione.

-   Se è disponibile un word breaker per la famiglia linguistica, ma non per una specifica lingua secondaria, viene utilizzata la lingua principale. Il word breaker francese viene ad esempio utilizzato anche per la gestione di testo redatto in francese canadese.
-   Se per una particolare lingua non sono disponibili word breaker, verrà utilizzato il word breaker della lingua neutra. Con il word breaker della lingua neutra, le parole vengono spezzate in corrispondenza di caratteri neutri, ad esempio spazi e segni di punteggiatura.

## <a name="get-the-list-of-supported-languages"></a>Ottenere l'elenco delle lingue supportate

Per visualizzare l'elenco delle lingue supportate dalla ricerca full-text di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente. La presenza di una lingua nell'elenco indica che per tale lingua sono registrati word breaker. 
  
```sql
SELECT * FROM sys.fulltext_languages
```

##  <a name="register"></a> Ottenere l'elenco dei word breaker registrati

Per potere usare i word breaker di una determinata lingua per la ricerca full-text, è necessario registrarli. Per i word breaker registrati, anche le risorse linguistiche associate, ovvero stemmer, parole non significative e thesaurus, diventano disponibili per le operazioni di indicizzazione e query full-text.

Per visualizzare l'elenco dei componenti word breaker registrati, usare l'istruzione seguente.

```sql
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```

Per altre opzioni e ulteriori informazioni, vedere [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md).
 
## <a name="if-you-add-or-remove-a-word-breaker"></a>Se si aggiunge o rimuove un word breaker  
Se si aggiunge, rimuove o modifica un word breaker, è necessario aggiornare l'elenco degli identificatori delle impostazioni locali (LCID) di Microsoft Windows supportati per l'indicizzazione e le query full-text. Per altre informazioni, vedere [Visualizzazione o modifica di word breaker e filtri registrati](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="default"></a> Impostare l'opzione default full-text language  
 Per le versioni localizzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] imposta l'opzione **default full-text language** sulla lingua del server, se esiste una corrispondenza appropriata. Per le versioni non localizzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'opzione **default full-text language** è impostata sull'inglese.  
  
 Quando si crea o modifica un indice full-text, è possibile specificare una lingua diversa per ogni colonna di indicizzazione full-text. Se per una colonna non è stata specificata alcuna lingua, il valore predefinito è quello dell'opzione di configurazione **default full-text language**.  
  
> [!NOTE]  
>  È necessario che a tutte le colonne elencate in una singola clausola di funzione per query full-text venga applicata la stessa lingua, a meno che nella query l'opzione LANGUAGE non sia specificata. La lingua utilizzata per la colonna indicizzata full-text oggetto della query determina l'analisi linguistica eseguita sugli argomenti dei predicati ([CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)) e delle funzioni ([CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)) delle query full-text.  
  
##  <a name="lang"></a> Scegliere la lingua per una colonna indicizzata  
 Quando si crea un indice full-text, è consigliabile specificare una lingua per ogni colonna indicizzata. Se non viene specificata alcuna lingua per una colonna, viene utilizzata quella predefinita di sistema. La lingua di una colonna determina il word breaker e lo stemmer utilizzati per l'indicizzazione di quella colonna. Anche il file del thesaurus di quella lingua verrà utilizzato dalle query full-text sulla colonna.  
  
 Quando si crea un indice full-text, è necessario considerare alcuni aspetti relativi alla scelta della lingua delle colonne. Tali considerazioni riguardano il modo in cui il testo viene suddiviso in token e quindi indicizzato dal motore di ricerca full-text. Per altre informazioni, vedere [Scelta di una lingua durante la creazione di un indice full-text](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
Per visualizzare la lingua del word breaker di colonne specifiche, eseguire l'istruzione seguente.
   
```sql 
SELECT language_id AS 'LCID' FROM sys.fulltext_index_columns;
```  

Per altre opzioni e ulteriori informazioni, vedere [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md).

##  <a name="tshoot"></a> Risolvere i problemi relativi agli errori di timeout del word breaking  
 Un errore di timeout del word breaking può verificarsi in diverse situazioni. Per informazioni su queste situazioni e su come rispondere, vedere [MSSQLSERVER_30053](../errors-events/mssqlserver-30053-database-engine-error.md).

### <a name="info-about-the-mssqlserver_30053-error"></a>Informazioni sull'errore MSSQLSERVER_30053
  
|Proprietà|valore|
|-|-|
|Nome prodotto|SQL Server|  
|ID evento|30053|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|FTXT_QUERY_E_WORDBREAKINGTIMEOUT|  
|Testo del messaggio|Timeout del word breaking per la stringa di query full-text. Questo problema può verificarsi se il word breaker impiega molto tempo per elaborare la stringa di query full-text o se è in esecuzione un numero elevato di query nel server. Provare a eseguire nuovamente la query in un carico ridotto.|  
  
#### <a name="explanation"></a>Spiegazione  
 Un errore di timeout del word breaking può verificarsi nelle situazioni seguenti:  
  
-   Il word breaker per il linguaggio di query non è configurato correttamente. Le impostazioni del Registro di sistema, ad esempio, non sono corrette.  
  
-   Il malfunzionamento del word breaker è dovuto a una stringa di query specifica.  
  
-   Il word breaker restituisce troppi dati per una stringa di query specifica. I dati in eccesso sono considerati un potenziale attacco con sovraccarico del buffer e di conseguenza viene arrestato il processo del daemon di filtri (fdhost.exe) che ospita i servizi di word breaking.  
  
-   La configurazione del processo del daemon di filtri non è corretta.  
  
     I problemi di configurazione più comuni sono rappresentati dalla scadenza della password o da criteri del dominio che impediscono l'accesso dell'account del daemon di filtri.  
  
-   Un carico di lavoro di query molto elevato è in esecuzione nell'istanza server. Ad esempio, il word breaker impiega molto tempo per elaborare la stringa della query full-text o un numero elevato di query sono in esecuzione nel server. Si tratta tuttavia della causa meno probabile.  
  
#### <a name="user-action"></a>Azione dell'utente  
 Selezionare l'azione dell'utente adatta alla probabile causa del timeout, come segue:  
  
|Possibile causa|Azione utente|  
|--------------------|-----------------|  
|Il word breaker per il linguaggio di query non è configurato correttamente.|Se si utilizza un word breaker di terze parti, è possibile che non sia stato registrato correttamente nel sistema operativo. In questo caso, registrare nuovamente il word breaker. Per altre informazioni, vedere [Ripristinare i word breaker usati dalla ricerca alla versione precedente](revert-the-word-breakers-used-by-search-to-the-previous-version.md).|  
|Il malfunzionamento del word breaker è dovuto a una stringa di query specifica.|Se il word breaker è supportato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], contattare il Servizio Supporto Tecnico Clienti Microsoft.|  
|Il word breaker restituisce troppi dati per una stringa di query specifica.|Se il word breaker è supportato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], contattare il Servizio Supporto Tecnico Clienti Microsoft.|  
|La configurazione del processo del daemon di filtri non è corretta.|Assicurarsi che venga utilizzata la password corrente e che i criteri di dominio non stiano impedendo l'accesso dell'account del daemon di filtri.|  
|Nell'istanza del server è in esecuzione un carico di lavoro molto elevato di query.|Provare a eseguire nuovamente la query in un carico ridotto.|  

##  <a name="impact"></a> Informazioni sull'impatto dei word breaker aggiornati  
 Ogni versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include in genere nuovi word breaker con regole linguistiche migliori e maggiore accuratezza rispetto alle versioni precedenti. È possibile che il comportamento dei nuovi word breaker sia leggermente diverso da quello dei word breaker negli indici full-text importati da versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
Questo aspetto è rilevante se si importa un catalogo full-text al momento dell'aggiornamento di un database alla versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una o più lingue utilizzate dagli indici full-text nel catalogo full-text potrebbero essere associate ai nuovi word breaker. Per altre informazioni, vedere [Aggiornamento della ricerca full-text](../../relational-databases/search/upgrade-full-text-search.md).  
 
## <a name="see-also"></a>Vedere anche  
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)    
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   

