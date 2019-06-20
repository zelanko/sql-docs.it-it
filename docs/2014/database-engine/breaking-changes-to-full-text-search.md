---
title: Modifiche di rilievo apportate alla ricerca Full-Text | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- full-text catalogs [SQL Server], breaking changes
- breaking changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: c55a6748-e5d9-4fdb-9a1f-714475a419c5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 45b13c29af6a9c5e82533a4b66213d1cb1b9dd15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62787759"
---
# <a name="breaking-changes-to-full-text-search"></a>Modifiche di rilievo alla ricerca full-text
  In questo argomento vengono descritte le modifiche di rilievo apportate alla ricerca full-text. Tali modifiche potrebbero interrompere il funzionamento di applicazioni, funzionalità o script basati su versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. È possibile che questi problemi si verifichino quando viene effettuato un aggiornamento. Per altre informazioni, vedere [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
## <a name="breaking-changes-in-full-text-search-in-includesssql14includessssql14-mdmd"></a>Modifiche di rilievo nella ricerca full-text in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Informazioni disponibili in futuro.  
  
## <a name="breaking-changes-in-full-text-search-in-includesssql11includessssql11-mdmd"></a>Modifiche di rilievo nella ricerca full-text in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="collation-changed-for-name-column-in-sysfulltextlanguages"></a>Regole di confronto modificate per la colonna name in sys.fulltext_languages  
 Le regole di confronto della colonna **name** nella vista del catalogo [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql) sono state modificate dalle regole di confronto fisse del database Resource nelle regole di confronto predefinite selezionate per l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Questa modifica consente di confrontare i valori nella colonna **name** quando si crea un join della vista [sys.syslanguages &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql) con **sys.fulltext_languages**. Ad esempio, è possibile eseguire una query per tutti i database dove l'opzione di configurazione full-text language è diversa dal linguaggio di database predefinito.  
  
## <a name="breaking-changes-in-full-text-search-in-sql-server-2008"></a>Modifiche di rilievo nella ricerca full-text in SQL Server 2008  
 Le modifiche di rilievo riportate di seguito vengono applicate alla ricerca full-text tra [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] e [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e versioni successive.  
  
|Funzionalità|Scenario|SQL Server 2005|SQL Server 2008 e versioni successive|  
|-------------|--------------|---------------------|----------------------------------------|  
|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) con tipi definiti dall'utente (UDT)|La chiave full-text è un tipo definito dall'utente (UDT) di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], ad esempio `MyType = char(1)`.|La chiave restituita è del tipo assegnato al tipo definito dall'utente (UDT).<br /><br /> Nell'esempio, si tratterà **char (1)** .|La chiave restituita è del tipo definito dall'utente (UDT). Nell'esempio, si tratterà **MyType**.|  
|*top_n_by_rank* parametro (di CONTAINSTABLE e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) [!INCLUDE[tsql](../includes/tsql-md.md)] istruzioni)|*top_n_by_rank* le query che utilizzano 0 come parametro.|Ha esito negativo e viene restituito un messaggio di errore indicante che è necessario utilizzare un valore maggiore di zero.|Ha esito positivo e vengono restituite zero righe.|  
|Le funzioni CONTAINSTABLE e **ItemCount**|Eliminare righe dalla tabella di base prima che vengano inserite modifiche in MSSearch.|Viene restituito un record fantasma da CONTAINSTABLE. **ItemCount** non viene modificato.|Non viene restituito alcun record fantasma da CONTAINSTABLE.|  
|**ItemCount**|Nella tabella sono contenuti documenti o colonne del tipo Null.|Oltre ai documenti indicizzati, vengono contati i documenti che sono null o che hanno tipi null per il **ItemCount** valore.|Vengono contati solo i documenti indicizzati per la **ItemCount** valore.|  
|Catalogo **ItemCount**|Colonna BLOB con estensione NULL.|Questa viene conteggiata **ItemCount** del catalogo|Non viene conteggiato **ItemCount** del catalogo.|  
|**UniqueKeyCount**|Esecuzione di una query su un conteggio di chiavi univoche da un catalogo, ad esempio due tabelle, tabella1 e tabella2, ciascuna con tre parole, parola1, parola2 e parola3.|**UniqueKeyCount** = 9. Nella tabella seguente viene descritto il modo in cui si ottiene questo valore:<br /><br /> tabella1 = 3<br /><br /> EOF per indice full-text di tabella1 = 1<br /><br /> tabella2 = 3<br /><br /> EOF per indice full-text di tabella2 = 1<br /><br /> Catalogo full-text = 1|Per ogni tabella, **UniqueKeyCount** è il numero di parole chiave distinct + 1 (0xFF).  Non considera le stesse parole in > 1 doc come nuova chiave univoca.<br /><br /> Per un catalogo **UniqueKeyCount** è la somma dei **UniqueKeyCount** della ognuno delle tabelle nel catalogo. Parole identiche di tabelle diverse vengono considerate chiavi univoche. In questo caso il conteggio di chiavi univoche è 8.|  
|**Pre-calcola classifica** opzione a livello di server|Ottimizzazione delle prestazioni delle query FREETEXTTABLE.|Quando l'opzione è impostata su 1, le query FREETEXTTABLE specificate con *top_n_by_rank* usare pre-calcolati classifica dati archiviati nei cataloghi full-text.|Non è supportata.|  
|[sp_fulltext_pendingchanges](/sql/relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql) quando si aggiorna una colonna chiave|Aggiornare la colonna chiave full-text in una riga di una tabella a 2 righe ed eseguire sp_fulltext_pendingchanges.|Vengono visualizzate entrambe le righe.|Viene visualizzata solo una riga.|  
|Funzioni inline|Funzioni inline con un operatore full-text|Viene restituito un messaggio di errore.|Vengono restituite le righe pertinenti.|  
|[sp_fulltext_database](/sql/relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql)|Abilitare o disabilitare la ricerca full-text utilizzando sp_fulltext_database.|Non viene restituito alcun risultato per le query full-text. Se la funzionalità full-text è disabilitata per il database, le operazioni full-text non sono consentite.|Restituisce risultati nelle query full-text e le operazioni full-text sono consentite, anche se la funzionalità full-text è disabilitata per il database.|  
|Parole non significative specifiche delle impostazioni locali|Esegue una query varianti inlocale specifiche della lingua padre, ad esempio francese (Belgio) e francese (Canada).|Le query specifiche inlocale varianti vengono elaborate dai componenti (word breaker, stemmer e parole non significative) della lingua padre. I componenti della lingua Francese (Francia), ad esempio, vengono utilizzati per l'analisi della lingua Francese (Belgio).|È necessario aggiungere in modo esplicito parole non significative per ogni identificatore delle impostazioni locali (LCID). È necessario, ad esempio, specificare un LCID per Belgio, Canada e Francia.|  
|Processo di stemming del thesaurus|Utilizzo del thesaurus e di forme flessive (stemming).|Viene eseguito lo stemming automatico di una parola del thesaurus in seguito all'espansione.|Se si desidera la forma flessiva nell'espansione, è necessario aggiungerla in modo esplicito.|  
|Percorso e filegroup del catalogo full-text|Utilizzo di cataloghi full-text.|Ogni catalogo full-text in cui è presente un percorso fisico, appartiene a un filegroup. e viene considerato un file di database.|Un catalogo full-text è un oggetto virtuale e non appartiene ad alcun filegroup. Un catalogo full-text è un concetto logico che fa riferimento a un gruppo di indici full-text.<br /><br /> Nota: [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)][!INCLUDE[tsql](../includes/tsql-md.md)] Le istruzioni DDL che specificano cataloghi full-text funzionano correttamente.|  
|[sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql)|Utilizzo del percorso, di data_space_id e di file_id nella vista del catalogo.|Queste colonne restituiscono un valore specifico.|Queste colonne restituiscono NULL perché il catalogo full-text non si trova più nel file system.|  
|[sys.sysfulltextcatalogs](/sql/relational-databases/system-compatibility-views/sys-sysfulltextcatalogs-transact-sql)|Utilizzo della colonna percorso di questa tabella di sistema deprecata.|Restituisce il percorso del file system del catalogo full-text.|Restituisce NULL perché il catalogo full-text non si trova più nel file system.|  
|[sp_help_fulltext_catalogs](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql)<br /><br /> [sp_help_fulltext_catalogs_cursor](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql)|Utilizzo della colonna PATH di queste stored procedure deprecate.|Restituisce il percorso del file system del catalogo full-text.|Restituisce NULL perché il catalogo full-text non si trova più nel file system.|  
|[sp_help_fulltext_catalog_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql)|Utilizzo di sp_help_fulltext_catalog_components di questa stored procedure.|Viene restituito un elenco di tutti i componenti (filtri, word breaker e gestori di protocollo) utilizzati per tutti i cataloghi full-text nel database corrente.|Vengono restituite righe vuote.|  
|[DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql)|Usando il **IsFullTextEnabled** proprietà.|Il **IsFullTextEnabled** impostazione indica se la ricerca full-text è abilitata in un database specifico.|Il valore di questa colonna non ha alcun effetto. I database utente sono sempre abilitati per la ricerca full-text.|  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche del comportamento di ricerca Full-Text](../relational-databases/search/full-text-search.md)   
 [Ricerca full-text](../relational-databases/search/full-text-search.md)  
  
  
