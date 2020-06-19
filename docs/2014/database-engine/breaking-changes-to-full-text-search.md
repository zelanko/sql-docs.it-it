---
title: Modifiche di rilievo alla ricerca full-text | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 260b1a303685ad9247154504400ef1519ecaa219
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936122"
---
# <a name="breaking-changes-to-full-text-search"></a>Modifiche di rilievo alla ricerca full-text
  In questo argomento vengono descritte le modifiche di rilievo apportate alla ricerca full-text. Tali modifiche potrebbero interrompere il funzionamento di applicazioni, funzionalità o script basati su versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. È possibile che questi problemi si verifichino quando viene effettuato un aggiornamento. Per altre informazioni, vedere [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
## <a name="breaking-changes-in-full-text-search-in-sssql14"></a>Modifiche di rilievo nella ricerca full-text in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Informazioni disponibili in futuro.  
  
## <a name="breaking-changes-in-full-text-search-in-sssql11"></a>Modifiche di rilievo nella ricerca full-text in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="collation-changed-for-name-column-in-sysfulltext_languages"></a>Regole di confronto modificate per la colonna name in sys.fulltext_languages  
 Le regole di confronto della colonna **name** nella vista del catalogo [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql) sono state modificate dalle regole di confronto fisse del database Resource nelle regole di confronto predefinite selezionate per l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Questa modifica consente di confrontare i valori nella colonna **name** quando si crea un join della vista [sys.syslanguages &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql) con **sys.fulltext_languages**. Ad esempio, è possibile eseguire una query per tutti i database dove l'opzione di configurazione full-text language è diversa dal linguaggio di database predefinito.  
  
## <a name="breaking-changes-in-full-text-search-in-sql-server-2008"></a>Modifiche di rilievo nella ricerca full-text in SQL Server 2008  
 Le modifiche di rilievo riportate di seguito vengono applicate alla ricerca full-text tra [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] e [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e versioni successive.  
  
|Funzionalità|Scenario|SQL Server 2005|SQL Server 2008 e versioni successive|  
|-------------|--------------|---------------------|----------------------------------------|  
|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) con tipi definiti dall'utente (UDT)|La chiave full-text è un tipo definito dall'utente (UDT) di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], ad esempio `MyType = char(1)`.|La chiave restituita è del tipo assegnato al tipo definito dall'utente (UDT).<br /><br /> Nell'esempio, questo sarebbe **char (1)**.|La chiave restituita è del tipo definito dall'utente (UDT). Nell'esempio, si tratta di **MyType**.|  
|*top_n_by_rank* parametro (delle istruzioni CONTAINSTABLE e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) [!INCLUDE[tsql](../includes/tsql-md.md)] )|*top_n_by_rank* le query che utilizzano 0 come parametro.|Ha esito negativo e viene restituito un messaggio di errore indicante che è necessario utilizzare un valore maggiore di zero.|Ha esito positivo e vengono restituite zero righe.|  
|CONTAINSTABLE e **ItemCount**|Eliminare righe dalla tabella di base prima che vengano inserite modifiche in MSSearch.|Viene restituito un record fantasma da CONTAINSTABLE. **ItemCount** non modificato.|Non viene restituito alcun record fantasma da CONTAINSTABLE.|  
|**ItemCount**|Nella tabella sono contenuti documenti o colonne del tipo Null.|Oltre ai documenti indicizzati, i documenti null o con tipi null vengono conteggiati nel valore **ItemCount** .|Solo i documenti indicizzati vengono conteggiati nel valore **ItemCount** .|  
|**ItemCount** Catalogo|Colonna BLOB con estensione NULL.|Viene conteggiata in **ItemCount** del catalogo|Non viene conteggiato in **ItemCount** di Catalog.|  
|**UniqueKeyCount**|Esecuzione di una query su un conteggio di chiavi univoche da un catalogo, ad esempio due tabelle, tabella1 e tabella2, ciascuna con tre parole, parola1, parola2 e parola3.|**UniqueKeyCount** = 9. Nella tabella seguente viene descritto il modo in cui si ottiene questo valore:<br /><br /> tabella1 = 3<br /><br /> EOF per indice full-text di tabella1 = 1<br /><br /> tabella2 = 3<br /><br /> EOF per indice full-text di tabella2 = 1<br /><br /> Catalogo full-text = 1|Per ogni tabella, **UniqueKeyCount** è il numero di parole chiave DISTINCT + 1 (0xFF).  Questa operazione non considera le stesse parole nel documento > 1 come nuova chiave univoca.<br /><br /> Per un catalogo, **UniqueKeyCount** è la somma di **UniqueKeyCount** di ciascuna tabella nel catalogo. Parole identiche di tabelle diverse vengono considerate chiavi univoche. In questo caso il conteggio di chiavi univoche è 8.|  
|opzione a livello di server **precompute rank**|Ottimizzazione delle prestazioni delle query FREETEXTTABLE.|Quando l'opzione è impostata su 1, le query FREETEXTTABLE specificate con *top_n_by_rank* utilizzano dati di rango pre-calcolati archiviati nei cataloghi full-text.|Non è supportata.|  
|[sp_fulltext_pendingchanges](/sql/relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql) durante l'aggiornamento della colonna chiave|Aggiornare la colonna chiave full-text in una riga di una tabella a 2 righe ed eseguire sp_fulltext_pendingchanges.|Vengono visualizzate entrambe le righe.|Viene visualizzata solo una riga.|  
|Funzioni inline|Funzioni inline con un operatore full-text|Viene restituito un messaggio di errore.|Vengono restituite le righe pertinenti.|  
|[sp_fulltext_database](/sql/relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql)|Abilitare o disabilitare la ricerca full-text utilizzando sp_fulltext_database.|Non viene restituito alcun risultato per le query full-text. Se la funzionalità full-text è disabilitata per il database, le operazioni full-text non sono consentite.|Restituisce risultati nelle query full-text e le operazioni full-text sono consentite, anche se la funzionalità full-text è disabilitata per il database.|  
|Parole non significative specifiche delle impostazioni locali|Esegue una query sulle varianti specifiche delle impostazioni locali di una lingua padre, ad esempio francese belga e francese (Canada).|Le query sulle varianti specifiche delle impostazioni locali vengono elaborate dai componenti (Word breaker, stemmer e parole non significative) della lingua padre. I componenti della lingua Francese (Francia), ad esempio, vengono utilizzati per l'analisi della lingua Francese (Belgio).|È necessario aggiungere in modo esplicito parole non significative per ogni identificatore delle impostazioni locali (LCID). È necessario, ad esempio, specificare un LCID per Belgio, Canada e Francia.|  
|Processo di stemming del thesaurus|Utilizzo del thesaurus e di forme flessive (stemming).|Viene eseguito lo stemming automatico di una parola del thesaurus in seguito all'espansione.|Se si desidera la forma flessiva nell'espansione, è necessario aggiungerla in modo esplicito.|  
|Percorso e filegroup del catalogo full-text|Utilizzo di cataloghi full-text.|Ogni catalogo full-text in cui è presente un percorso fisico, appartiene a un filegroup. e viene considerato un file di database.|Un catalogo full-text è un oggetto virtuale e non appartiene ad alcun filegroup. Un catalogo full-text è un concetto logico che fa riferimento a un gruppo di indici full-text.<br /><br /> Nota: le [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)] istruzioni DDL che specificano i cataloghi full-text funzionano correttamente.|  
|[sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql)|Utilizzo del percorso, di data_space_id e di file_id nella vista del catalogo.|Queste colonne restituiscono un valore specifico.|Queste colonne restituiscono NULL perché il catalogo full-text non si trova più nel file system.|  
|[sys.sysfulltextcatalogs](/sql/relational-databases/system-compatibility-views/sys-sysfulltextcatalogs-transact-sql)|Utilizzo della colonna percorso di questa tabella di sistema deprecata.|Restituisce il percorso del file system del catalogo full-text.|Restituisce NULL perché il catalogo full-text non si trova più nel file system.|  
|[sp_help_fulltext_catalogs](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql)<br /><br /> [sp_help_fulltext_catalogs_cursor](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql)|Utilizzo della colonna PATH di queste stored procedure deprecate.|Restituisce il percorso del file system del catalogo full-text.|Restituisce NULL perché il catalogo full-text non si trova più nel file system.|  
|[sp_help_fulltext_catalog_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql)|Utilizzo di sp_help_fulltext_catalog_components di questa stored procedure.|Viene restituito un elenco di tutti i componenti (filtri, word breaker e gestori di protocollo) utilizzati per tutti i cataloghi full-text nel database corrente.|Vengono restituite righe vuote.|  
|[DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql)|Utilizzando la proprietà **IsFullTextEnabled** .|L'impostazione **IsFullTextEnabled** indica se la ricerca full-text è abilitata in un determinato database.|Il valore di questa colonna non ha alcun effetto. I database utente sono sempre abilitati per la ricerca full-text.|  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche del comportamento nella ricerca full-text](../relational-databases/search/full-text-search.md)   
 [Ricerca full-text](../relational-databases/search/full-text-search.md)  
  
  
