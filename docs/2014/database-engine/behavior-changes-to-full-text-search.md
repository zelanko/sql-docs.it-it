---
title: Modifiche del comportamento di ricerca Full-Text | Microsoft Docs
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
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 0d3bf42ec031415d16ea45bc8241c85c6d937c35
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813194"
---
# <a name="behavior-changes-to-full-text-search"></a>Differenze di comportamento nella ricerca full-text
  In questo argomento vengono descritte le modifiche del comportamento nella ricerca full-text. Queste modifiche influiscono sulle modalità di utilizzo o di interazione delle funzionalità in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] rispetto alle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="behavior-changes-in-full-text-search-in-includesssql14includessssql14-mdmd"></a>Modifiche del comportamento nella ricerca full-text in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Informazioni disponibili in futuro.  
  
## <a name="behavior-changes-in-full-text-search-in-includesssql11includessssql11-mdmd"></a>Modifiche del comportamento nella ricerca full-text in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 In [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] viene installata una nuova versione dei word breaker e degli stemmer per l'Inglese (Stati Uniti), LCID 1033, e l'Inglese (Regno Unito), LCID 2057. È tuttavia possibile passare alla versione precedente di questi componenti se si desidera mantenere il comportamento precedente. Per altre informazioni vedere [Modifica del word breaker utilizzato per le lingue Inglese (Stati Uniti) e Inglese (Regno Unito)](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).  
  
### <a name="new-word-breakers-and-stemmers-installed"></a>Installazione di word breaker e stemmer nuovi  
 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] consente di aggiornare tutti i word breaker e stemmer utilizzati dalla ricerca full-text e semantica. Per coerenza tra il contenuto di indici e i risultati di query, si consiglia di ripopolare gli indici full-text esistenti.  
  
1.  Sono disponibili word breaker nuovi per l'inglese. Se è necessario mantenere il comportamento precedente, vedere [Modifica del word breaker utilizzato per le lingue Inglese (Stati Uniti) e Inglese (Regno Unito)](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).  
  
2.  I word breaker di terze parti per il danese, il polacco e il turco inclusi con le versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sono stati sostituiti con i componenti [!INCLUDE[msCoName](../includes/msconame-md.md)] . I nuovi componenti sono abilitati per impostazione predefinita.  
  
3.  Sono disponibili word breaker nuovi per il ceco e il greco. Nelle versioni precedenti della ricerca full-text di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non è incluso il supporto per queste due lingue.  
  
### <a name="behavior-changes-of-new-word-breakers-and-stemmers"></a>Modifiche di comportamento dei nuovi word breaker e stemmer  
 I nuovi componenti potrebbero restituire risultati diversi rispetto ai componenti meno recenti quando si popola e si esegue una query sugli indici full-text. Nelle tabelle seguenti si illustrano alcune delle possibili differenze nei risultati in lingua inglese.  
  
 Se è necessario mantenere il comportamento precedente dei word breaker e degli stemmer, vedere gli argomenti seguenti:  
  
-   [Modificare il word breaker usato per le lingue Inglese (Stati Uniti) e Inglese (Regno Unito)](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
-   [Ripristinare i word breaker usati dalla ricerca alla versione precedente](../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
 In alcuni casi, i nuovi componenti restituiscono *più* risultati:  
  
|**Nome**|**Risultati con word breaker precedente e dello stemmer**|**Risultati con i nuovi word breaker e stemmer**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|cat-dog|cat<br /><br /> dog|cat<br /><br /> cat-dog<br /><br /> dog|  
|cat@dog.com|cat<br /><br /> com<br /><br /> dog|cat<br /><br /> cat@dog.com<br /><br /> com<br /><br /> dog|  
|12/11/2011<br /><br /> *(dove il termine è una data)*|12/11/2011<br /><br /> dd20111211|11<br /><br /> 12<br /><br /> 12/11/2011<br /><br /> 2011<br /><br /> dd20111211|  
  
 In alcuni casi, i nuovi componenti restituiscono risultati *simili* :  
  
|**Nome**|**Risultati con word breaker precedente e dello stemmer**|**Risultati con i nuovi word breaker e stemmer**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|100$|100$<br /><br /> nn100$|100$<br /><br /> nn100usd|  
|022|022<br /><br /> nn022|022<br /><br /> nn22|  
|10:49AM<br /><br /> *(in cui il termine è un'ora)*|10:49AM<br /><br /> tt1049|10:49AM<br /><br /> tt24104900|  
  
 In alcuni casi i nuovi componenti restituiscono *pochi* risultati o risultati non previsti dalle applicazioni:  
  
|**Nome**|**Risultati con word breaker precedente e dello stemmer**|**Risultati con i nuovi word breaker e stemmer**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|jěˊÿｑℭžl<br /><br /> *(in cui le condizioni non sono caratteri validi in lingua inglese)*|'jěˊÿｑℭžl'|je yq zl|  
|table's|table's<br /><br /> table|table's|  
|cat-|cat<br /><br /> cat-|cat|  
|v-z *(dove v e z sono parole non significative)*|*(Nessun risultato)*|v-z|  
|$100 000 USD|$100<br /><br /> 000<br /><br /> nn000<br /><br /> nn100$<br /><br /> usd|$100 000 USD<br /><br /> nn100000usd|  
|beautiful U.S land|beautiful<br /><br /> land<br /><br /> u.s<br /><br /> us|beautiful<br /><br /> land|  
|Mt. Kent and Mt Challenger|challenger<br /><br /> kent<br /><br /> mt<br /><br /> Mt.|mt<br /><br /> kent<br /><br /> challenger|  
  
## <a name="behavior-changes-in-full-text-search-in-sql-server-2008"></a>Modifiche del comportamento nella ricerca full-text in SQL Server 2008  
 In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e versioni successive, il motore Full-Text è integrato come servizio di database nel database relazionale come parte dell'infrastruttura del server query e l'archiviazione del motore. L'architettura della nuova ricerca full-text consente di raggiungere i seguenti obiettivi:  
  
-   Archiviazione integrata e ricerca di gestione-Full-text è ora integrata direttamente con le funzionalità intrinseche di archiviazione e la gestione degli [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], e il servizio MSFTESQL non esiste più.  
  
    -   Gli indici full-text vengono archiviati nei filegroup del database, anziché nel file system. Le operazioni amministrative su un database, ad esempio la creazione di un backup, influiscono automaticamente sugli indici full-text.  
  
    -   Un catalogo full-text è ora un oggetto virtuale che non appartiene ad alcun filegroup. Si tratta di un concetto logico che fa riferimento a un gruppo di indici full-text. Pertanto, molte funzionalità di gestione dei cataloghi sono state deprecate comportando modifiche di rilievo per alcune funzionalità. Per altre informazioni, vedere [funzionalità del motore di Database deprecate in SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md) e [modifiche di rilievo alla ricerca Full-Text](breaking-changes-to-full-text-search.md).  
  
        > [!NOTE]  
        >  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)] Le istruzioni DDL che specificano cataloghi full-text funzionano correttamente.  
  
-   L'elaborazione, il nuovo processore di query ricerca full-text integrata query fa parte del motore di Database ed è completamente integrato con il processore di Query di SQL Server. Ciò significa che Query Optimizer riconosce i predicati di query full-text eseguendoli automaticamente nel modo più efficiente possibile.  
  
-   Amministrazione migliorata e integrate nella risoluzione dei problemi di ricerca full-text fornisce strumenti che consentono di analizzare le strutture di ricerca, ad esempio l'indice full-text, l'output di un word breaker specifico, configurazione di parole non significative e così via.  
  
-   I file di parole non significative sono stati sostituiti dagli elenchi di parole non significative. Un elenco di parole non significative è un oggetto di database tramite cui vengono facilitate le attività di gestibilità delle parole non significative e migliorata l'integrità tra istanze e ambienti del server diversi. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e versioni successive sono disponibili nuovi word breaker per molte delle lingue presenti in [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]. Solo i word breaker per inglese, coreano, tailandese e cinese (tutti i tipi) restano invariati. Per altre lingue, se un catalogo full-text è stato importato durante una [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] database è stato aggiornato a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] o versione successiva, uno o più lingue utilizzate dagli indici full-text nel catalogo full-text potrebbero essere associate ai nuovi word breaker che potrebbe comportarsi in modo leggermente diverso dal word breaker importati. Per altre informazioni su come garantire la coerenza tra le query e il contenuto dell'indice full-text, vedere [aggiornamento della ricerca Full-Text](../relational-databases/search/upgrade-full-text-search.md).  
  
-   È stato aggiunto un nuovo servizio per l'utilità di avvio FDHOST (MSSQLFDLauncher). Per altre informazioni, vedere [Introduzione a ricerca Full-Text](../relational-databases/search/get-started-with-full-text-search.md).  
  
-   L'indicizzazione full-text funziona con un [FILESTREAM](../relational-databases/blob/filestream-sql-server.md) colonna nello stesso modo cui avviene una `varbinary(max)` colonna. La tabella FILESTREAM deve avere una colonna che contiene l'estensione del nome file per ogni BLOB FILESTREAM. Per altre informazioni, vedere [Query con ricerca Full-Text](../relational-databases/search/query-with-full-text-search.md),[configurare e gestire filtri per la ricerca](../relational-databases/search/configure-and-manage-filters-for-search.md), e [fulltext_document_types &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).  
  
     Il motore full-text consente di indicizzare il contenuto dei BLOB FILESTREAM. L'indicizzazione di file di immagini, ad esempio, potrebbe non essere utile. Un BLOB FILESTREAM viene reindicizzato quando viene aggiornato.  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca full-text](../relational-databases/search/full-text-search.md)   
 [Compatibilità con le versioni precedenti di ricerca full-Text](../../2014/database-engine/full-text-search-backward-compatibility.md)   
 [Aggiornamento della ricerca Full-Text](../relational-databases/search/upgrade-full-text-search.md)   
 [Introduzione alla ricerca full-text](../relational-databases/search/get-started-with-full-text-search.md)  
  
  
