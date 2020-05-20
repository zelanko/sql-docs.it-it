---
title: Modifiche del comportamento nella ricerca full-text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- behavior changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: 573444e8-51bc-4f3d-9813-0037d2e13b8f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 00dc0fbda03bb7f729123a84e7e91fb2361aee9f
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83001078"
---
# <a name="behavior-changes-to-full-text-search"></a>Differenze di comportamento nella ricerca full-text
  In questo argomento vengono descritte le modifiche del comportamento nella ricerca full-text. Queste modifiche influiscono sulle modalità di utilizzo o di interazione delle funzionalità in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] rispetto alle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="behavior-changes-in-full-text-search-in-sssql14"></a>Modifiche del comportamento nella ricerca full-text in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Informazioni disponibili in futuro.  
  
## <a name="behavior-changes-in-full-text-search-in-sssql11"></a>Modifiche del comportamento nella ricerca full-text in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 In [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] viene installata una nuova versione dei word breaker e degli stemmer per l'Inglese (Stati Uniti), LCID 1033, e l'Inglese (Regno Unito), LCID 2057. È tuttavia possibile passare alla versione precedente di questi componenti se si desidera mantenere il comportamento precedente. Per altre informazioni vedere [Modifica del word breaker utilizzato per le lingue Inglese (Stati Uniti) e Inglese (Regno Unito)](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).  
  
### <a name="new-word-breakers-and-stemmers-installed"></a>Installazione di word breaker e stemmer nuovi  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] consente di aggiornare tutti i word breaker e stemmer utilizzati dalla ricerca full-text e semantica. Per coerenza tra il contenuto di indici e i risultati di query, si consiglia di ripopolare gli indici full-text esistenti.  
  
1.  Sono disponibili word breaker nuovi per l'inglese. Se è necessario mantenere il comportamento precedente, vedere [Modifica del word breaker utilizzato per le lingue Inglese (Stati Uniti) e Inglese (Regno Unito)](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).  
  
2.  I word breaker di terze parti per il danese, il polacco e il turco inclusi con le versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sono stati sostituiti con i componenti [!INCLUDE[msCoName](../includes/msconame-md.md)] . I nuovi componenti sono abilitati per impostazione predefinita.  
  
3.  Sono disponibili word breaker nuovi per il ceco e il greco. Nelle versioni precedenti della ricerca full-text di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non è incluso il supporto per queste due lingue.  
  
### <a name="behavior-changes-of-new-word-breakers-and-stemmers"></a>Modifiche di comportamento dei nuovi word breaker e stemmer  
 I nuovi componenti potrebbero restituire risultati diversi rispetto ai componenti meno recenti quando si popola e si esegue una query sugli indici full-text. Nelle tabelle seguenti si illustrano alcune delle possibili differenze nei risultati in lingua inglese.  
  
 Se è necessario mantenere il comportamento precedente dei word breaker e degli stemmer, vedere gli argomenti seguenti:  
  
-   [Modifica del word breaker utilizzato per le lingue Inglese (Stati Uniti) e Inglese (Regno Unito)](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
-   [Ripristinare i word breaker utilizzati dalla ricerca alla versione precedente](../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
 In alcuni casi, i nuovi componenti restituiscono *più* risultati:  
  
|**Termine**|**Risultati con word breaker e stemmer precedenti**|**Risultati con word breaker e stemmer nuovi**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|cat-dog|cat<br /><br /> dog|cat<br /><br /> cat-dog<br /><br /> dog|  
|cat@dog.com|cat<br /><br /> com<br /><br /> dog|cat<br /><br /> cat@dog.com<br /><br /> com<br /><br /> dog|  
|12/11/2011<br /><br /> *(dove il nome è una data)*|12/11/2011<br /><br /> dd20111211|11<br /><br /> 12<br /><br /> 12/11/2011<br /><br /> 2011<br /><br /> dd20111211|  
  
 In alcuni casi, i nuovi componenti restituiscono risultati *simili* :  
  
|**Termine**|**Risultati con word breaker e stemmer precedenti**|**Risultati con word breaker e stemmer nuovi**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|100$|100$<br /><br /> nn100$|100$<br /><br /> nn100usd|  
|022|022<br /><br /> nn022|022<br /><br /> nn22|  
|10:49AM<br /><br /> *(dove il nome è un'ora)*|10:49AM<br /><br /> tt1049|10:49AM<br /><br /> tt24104900|  
  
 In alcuni casi i nuovi componenti restituiscono *pochi* risultati o risultati non previsti dalle applicazioni:  
  
|**Termine**|**Risultati con word breaker e stemmer precedenti**|**Risultati con word breaker e stemmer nuovi**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|jě ˊ ÿqCžl<br /><br /> *(dove i nomi sono caratteri inglesi non validi)*|' jě ˊ ÿqCžl '|je yq zl|  
|table's|table's<br /><br /> tabella|table's|  
|cat-|cat<br /><br /> cat-|cat|  
|v-z *(dove v e z sono parole non significative)*|*(nessun risultato)*|v-z|  
|$100 000 USD|$100<br /><br /> 7000<br /><br /> nn000<br /><br /> nn100$<br /><br /> usd|$100 000 USD<br /><br /> nn100000usd|  
|beautiful U.S land|beautiful<br /><br /> land<br /><br /> u.s<br /><br /> us|beautiful<br /><br /> land|  
|Mt. Kent and Mt Challenger|challenger<br /><br /> kent<br /><br /> mt<br /><br /> Mt.|mt<br /><br /> kent<br /><br /> challenger|  
  
## <a name="behavior-changes-in-full-text-search-in-sql-server-2008"></a>Modifiche del comportamento nella ricerca full-text in SQL Server 2008  
 In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e versioni successive il motore di ricerca full-text è integrato come servizio di database nel database relazionale come parte dell'infrastruttura del motore di archiviazione e di query del server. L'architettura della nuova ricerca full-text consente di raggiungere i seguenti obiettivi:  
  
-   Archiviazione e gestione integrate: la ricerca full-text è ora integrata direttamente con le funzionalità intrinseche di archiviazione e gestione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e il servizio MSFTESQL non esiste più.  
  
    -   Gli indici full-text vengono archiviati nei filegroup del database, anziché nel file system. Le operazioni amministrative su un database, ad esempio la creazione di un backup, influiscono automaticamente sugli indici full-text.  
  
    -   Un catalogo full-text è ora un oggetto virtuale che non appartiene ad alcun filegroup. Si tratta di un concetto logico che fa riferimento a un gruppo di indici full-text. Pertanto, molte funzionalità di gestione dei cataloghi sono state deprecate comportando modifiche di rilievo per alcune funzionalità. Per ulteriori informazioni, vedere [deprecated motore di database features in SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md) e [modifiche di rilievo alla ricerca full-text](breaking-changes-to-full-text-search.md).  
  
        > [!NOTE]  
        >  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)]Le istruzioni DDL  di  che specificano cataloghi full-text funzionano correttamente.  
  
-   Elaborazione delle query integrata: il nuovo elaboratore di query di ricerca full-text fa parte della motore di database ed è completamente integrato con SQL Server query processor. Ciò significa che Query Optimizer riconosce i predicati di query full-text eseguendoli automaticamente nel modo più efficiente possibile.  
  
-   Amministrazione migliorata e risoluzione dei problemi: la ricerca full-text integrata fornisce strumenti che consentono di analizzare le strutture di ricerca, ad esempio l'indice full-text, l'output di un Word breaker specifico, la configurazione di parola non significativa e così via.  
  
-   I file di parole non significative sono stati sostituiti dagli elenchi di parole non significative. Un elenco di parole non significative è un oggetto di database tramite cui vengono facilitate le attività di gestibilità delle parole non significative e migliorata l'integrità tra istanze e ambienti del server diversi. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e versioni successive sono disponibili nuovi word breaker per molte delle lingue presenti in [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]. Solo i word breaker per inglese, coreano, tailandese e cinese (tutti i tipi) restano invariati. Per altre lingue, se un catalogo full-text è stato importato quando un [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] database è stato aggiornato a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] o versione successiva, è possibile che una o più lingue utilizzate dagli indici full-text nel catalogo full-text siano ora associate ai nuovi word breaker che potrebbero comportarsi in modo leggermente diverso dai Word breaker importati. Per ulteriori informazioni su come garantire la coerenza tra le query e il contenuto dell'indice full-text, vedere [aggiornamento della ricerca full-text](../relational-databases/search/upgrade-full-text-search.md).  
  
-   È stato aggiunto un nuovo servizio per l'utilità di avvio FDHOST (MSSQLFDLauncher). Per ulteriori informazioni, vedere la pagina relativa all' [Introduzione alla ricerca full-text](../relational-databases/search/get-started-with-full-text-search.md).  
  
-   L'indicizzazione full-text funziona con una colonna [FileStream](../relational-databases/blob/filestream-sql-server.md) nello stesso modo in cui avviene per una `varbinary(max)` colonna. La tabella FILESTREAM deve avere una colonna che contiene l'estensione del nome file per ogni BLOB FILESTREAM. Per ulteriori informazioni, vedere [eseguire query con ricerca full-text](../relational-databases/search/query-with-full-text-search.md),[configurare e gestire filtri per la ricerca](../relational-databases/search/configure-and-manage-filters-for-search.md)e [sys. FULLTEXT_DOCUMENT_TYPES &#40;&#41;Transact-SQL ](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).  
  
     Il motore full-text consente di indicizzare il contenuto dei BLOB FILESTREAM. L'indicizzazione di file di immagini, ad esempio, potrebbe non essere utile. Un BLOB FILESTREAM viene reindicizzato quando viene aggiornato.  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca full-text](../relational-databases/search/full-text-search.md)   
 [Compatibilità con le versioni precedenti della ricerca full-text](../../2014/database-engine/full-text-search-backward-compatibility.md)   
 [Aggiornare la ricerca full-text](../relational-databases/search/upgrade-full-text-search.md)   
 [Introduzione alla ricerca full-text](../relational-databases/search/get-started-with-full-text-search.md)  
  
  
