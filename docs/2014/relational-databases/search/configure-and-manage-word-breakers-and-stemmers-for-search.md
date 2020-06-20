---
title: Configurare e gestire word breaker e stemmer per la ricerca | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 22cb7371a0215989d2759ddfb2c84f51ba5c3c31
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84997584"
---
# <a name="configure-and-manage-word-breakers-and-stemmers-for-search"></a>Configurazione e gestione di word breaker e stemmer per la ricerca
  Word breaker e stemmer eseguono l'analisi linguistica su tutti i dati con indicizzazione full-text. L'analisi linguistica riguarda la ricerca dell'inizio e della fine delle parole (isolamento delle parole) e la coniugazione dei verbi (flessione). Word breaker e stemmer sono specifici della lingua e le regole per l'analisi linguistica variano a seconda della lingua. Un *word breaker* identifica singole parole determinando i delimitatori di parola in base alle regole lessicali della lingua. Ogni parola ( *token*) viene inserita nell'indice full-text utilizzando una rappresentazione compressa per ridurre le relative dimensioni. Lo *stemmer* genera forme flessive di una particolare parola in base alle regole di quella lingua, ad esempio "running", "ran" e "runner" sono varie forme della parola "run".  
  
 L'utilizzo di word breaker specifici di ogni lingua consente una maggiore accuratezza dei termini risultanti per le diverse lingue. Se è disponibile un word breaker per la famiglia linguistica, ma non per una specifica lingua secondaria, viene utilizzata la lingua principale. Il word breaker francese viene ad esempio utilizzato anche per la gestione di testo redatto in francese canadese. Se per una particolare lingua non sono disponibili word breaker, verrà utilizzato il word breaker della lingua neutra. Con il word breaker della lingua neutra, le parole vengono spezzate in corrispondenza di caratteri neutri, ad esempio spazi e segni di punteggiatura.  
  
##  <a name="registering-word-breakers"></a><a name="register"></a>Registrazione di Word breaker  
 Per potere utilizzare i word breaker di una determinata lingua, è necessario registrarli. Per i Word breaker registrati, le risorse linguistiche associate, ovvero stemmer, parole non significative (parole non significative) e file del thesaurus, diventano disponibili anche per le operazioni di indicizzazione e query full-text. Per visualizzare un elenco delle lingue i cui word breaker sono attualmente registrati con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilizzare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente:  
  
 SELECT * FROM sys.fulltext_languages  
  
 Se si aggiunge, rimuove o modifica un word breaker, è necessario aggiornare l'elenco degli identificatori delle impostazioni locali (LCID) di Microsoft Windows supportati per l'indicizzazione e le query full-text. Per altre informazioni, vedere [Visualizzazione o modifica di word breaker e filtri registrati](view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="setting-the-default-full-text-language-option"></a><a name="default"></a>Impostazione dell'opzione default full-text language  
 Per una versione localizzata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il programma di installazione di imposta l' `default full-text language` opzione sulla lingua del server, se esiste una corrispondenza appropriata. Per le versioni non localizzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'opzione `default full-text language` è impostata sull'inglese.  
  
 Quando si crea o modifica un indice full-text, è possibile specificare una lingua diversa per ogni colonna di indicizzazione full-text. Se per una colonna non è stata specificata alcuna lingua, il valore predefinito è quello dell'opzione di configurazione `default full-text language`.  
  
> [!NOTE]  
>  È necessario che a tutte le colonne elencate in una singola clausola di funzione per query full-text venga applicata la stessa lingua, a meno che nella query l'opzione LANGUAGE non sia specificata. La lingua utilizzata per la colonna indicizzata full-text oggetto della query determina l'analisi linguistica eseguita sugli argomenti dei predicati ([CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)) e delle funzioni ([CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) e [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql)) delle query full-text.  
  
##  <a name="choosing-the-language-for-an-indexed-column"></a><a name="lang"></a>Scelta della lingua per una colonna indicizzata  
 Quando si crea un indice full-text, è consigliabile specificare una lingua per ogni colonna indicizzata. Se non viene specificata alcuna lingua per una colonna, viene utilizzata quella predefinita di sistema. La lingua di una colonna determina il word breaker e lo stemmer utilizzati per l'indicizzazione di quella colonna. Anche il file del thesaurus di quella lingua verrà utilizzato dalle query full-text sulla colonna.  
  
 Quando si crea un indice full-text, è necessario considerare alcuni aspetti relativi alla scelta della lingua delle colonne. Tali considerazioni riguardano il modo in cui il testo viene suddiviso in token e quindi indicizzato dal motore di ricerca full-text. Per altre informazioni, vedere [Scelta di una lingua durante la creazione di un indice full-text](choose-a-language-when-creating-a-full-text-index.md).  
  
 **Per visualizzare la lingua del word breaker di una colonna**  
  
-   [Gestione di indici full-text.](../indexes/indexes.md)  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
    ```  
    SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;  
    ```  
  
##  <a name="obtaining-information-about-word-breakers"></a><a name="info"></a>Recupero di informazioni sui Word breaker  
 **Visualizzazione del risultato della suddivisione in token di una combinazione di word breaker, thesaurus ed elenco di parole non significative**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql).  
  
 **Per restituire informazioni sui word breaker registrati**  
  
-   [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql)  
  
##  <a name="troubleshooting-word-breaking-time-out-errors"></a><a name="tshoot"></a>Risoluzione degli errori di timeout di suddivisione delle parole  
 Un errore di timeout del word breaking potrebbe verificarsi in diverse situazioni. Per informazioni su queste situazioni e su come rispondere, vedere [MSSQLSERVER_30053](../errors-events/mssqlserver-30053-database-engine-error.md).  
  
##  <a name="understanding-the-impact-of-new-word-breakers"></a><a name="impact"></a>Informazioni sull'effetto dei nuovi word breaker  
 Ogni versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include in genere nuovi word breaker con regole linguistiche migliori e maggiore accuratezza rispetto alle versioni precedenti. È possibile che il comportamento dei nuovi word breaker sia leggermente diverso da quello dei word breaker negli indici full-text importati da versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo aspetto è rilevante se si importa un catalogo full-text al momento dell'aggiornamento di un database alla versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una o più lingue utilizzate dagli indici full-text nel catalogo full-text potrebbero essere associate ai nuovi word breaker. Per altre informazioni, vedere [Aggiornamento della ricerca full-text](upgrade-full-text-search.md).  
  
 Per un elenco completo di tutti i word breaker, vedere [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [sp_fulltext_service &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)   
 [sys. fulltext_languages &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [Configurare e gestire parole non significative e elenchi per la ricerca full-text](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Aggiornamento della ricerca full-text](upgrade-full-text-search.md)  
  
  
