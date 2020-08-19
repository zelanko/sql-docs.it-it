---
description: Scelta di una lingua durante la creazione di un indice full-text
title: Scegliere una lingua durante la creazione di un indice full-text| Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- full-text indexes [SQL Server], languages
- international considerations [full-text search]
- stemmers [full-text search]
- global considerations [full-text search]
- full-text search [SQL Server], international considerations
- languages [SQL Server], full-text indexes
- word breakers [full-text search]
ms.assetid: 670a5181-ab80-436a-be96-d9498fbe2c09
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9f8c0860bb5ef874a6095b993478fa9cbc117fc4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475539"
---
# <a name="choose-a-language-when-creating-a-full-text-index"></a>Scelta di una lingua durante la creazione di un indice full-text

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Quando si crea un indice full-text, è necessario specificare una lingua a livello di colonna per la colonna indicizzata. Il [word breaker e gli stemmer](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) della lingua specificata verranno usati dalle query full-text sulla colonna. Quando si crea un indice full-text, è necessario considerare alcuni aspetti relativi alla scelta della lingua delle colonne. Tali considerazioni riguardano il modo in cui il testo viene suddiviso in token e quindi indicizzato dal motore di ricerca full-text.  
  
> [!NOTE]  
>  Per specificare una lingua a livello di colonna per una colonna di un indice full-text, usare la clausola *language_term* LANGUAGE quando si specifica la colonna. Per altre informazioni, vedere [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md) e [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
##  <a name="language-support-in-full-text-search"></a><a name="langsupp"></a> Supporto della lingua nella ricerca full-text  
 In questa sezione viene fornita un'introduzione ai word breaker e agli stemmer e viene illustrato l'utilizzo dell'LCID della lingua a livello di colonna da parte della ricerca full-text.  
  
### <a name="introduction-to-word-breakers-and-stemmers"></a>Introduzione ai word breaker e agli stemmer  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive è inclusa una nuova famiglia completa di word breaker e stemmer, notevolmente migliorati rispetto a quelli disponibili in precedenza in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Microsoft Natural Language Group (MS NLG) ha implementato e supporta questi nuovi componenti linguistici.  
  
 I nuovi word breaker offrono i vantaggi seguenti:  
  
-   Efficienza  
  
     I test effettuati hanno dimostrato che i nuovi word breaker sono affidabili anche negli ambienti di elaborazione query più complessi.  
  
-   Sicurezza  
  
     I nuovi word breaker sono abilitati per impostazione predefinita in SQL Server grazie ai miglioramenti della sicurezza nei componenti linguistici. È vivamente consigliabile che i componenti esterni quali word breaker e filtri vengano firmati per migliorare la sicurezza e l'affidabilità di SQL Server. È possibile configurare la funzionalità full-text per verificare che questi componenti siano firmati come descritto di seguito:  
  
    ```  
    EXEC sp_fulltext_service 'verify_signature';  
    ```  
  
-   Qualità  
  
     I word breaker sono di nuova progettazione e i test effettuati hanno dimostrato una qualità semantica migliore rispetto a quella dei word breaker precedenti. Ne risulta una maggiore accuratezza delle chiamate.  
  
-   I word breaker, disponibili per numerose lingue, sono inclusi direttamente in SQL Server e abilitati per impostazione predefinita.  
  
 Per un elenco delle lingue per le quali SQL Server include un word breaker e stemmer, vedere [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
  
### <a name="how-full-text-search-uses-the-name-of-the-column-level-language"></a>Utilizzo del nome della lingua a livello di colonna da parte della ricerca full-text  
 Quando si crea un indice full-text, è necessario specificare un nome di lingua valido per ogni colonna. Se un nome di lingua è valido, ma non restituito dalla vista del catalogo [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) , la ricerca full-text opta per il nome di lingua disponibile più simile nella stessa famiglia, se disponibile. Se non è disponibile una lingua simile, viene specificato il word breaker neutro. Questo comportamento potrebbe influire negativamente sull'accuratezza delle chiamate. Per creare un indice full-text, è pertanto consigliabile specificare un nome di lingua valido e disponibile per ogni colonna.  
  
> [!NOTE]  
>  L'identificatore LCID viene usato per tutti i tipi di dati considerati idonei per l'indicizzazione full-text, ad esempio **char** o **nchar**. Se l'ordinamento di una colonna di tipo **char**, **varchar**o **text** è impostato su una lingua diversa da quella identificata dall'LCID, quest'ultimo verrà usato comunque durante l'indicizzazione full-text e le query di quelle colonne.  
  
  
##  <a name="word-breaking"></a><a name="breaking"></a> Word breaking  
 Un word breaker ha la funzione di suddividere in token il testo da indicizzare in base ai delimitatori delle parole specifici della lingua. Il comportamento del word breaker varierà pertanto a seconda della lingua scelta. Se si usa una lingua, x, per indicizzare più lingue, {x, y e z}, è possibile che si verifichino risultati imprevisti. È ad esempio possibile che un elemento di interruzione delle parole quale il trattino (-) o la virgola (,) venga eliminato in una lingua, ma non in un'altra. In alcuni casi, si potrebbe inoltre ottenere un comportamento imprevisto per lo stemming, in quanto è possibile che a una determinata parola venga applicato uno stemmer diverso nelle diverse lingue. Nella lingua inglese, ad esempio, i delimitatori delle parole sono dati in genere da spazi o da elementi di punteggiatura. In altre lingue come il tedesco, invece, le parole o i caratteri vengono spesso uniti insieme. La lingua a livello di colonna scelta dovrebbe pertanto rappresentare la lingua che si desidera venga archiviata nelle righe di quella colonna.  
  
### <a name="western-languages"></a>Lingue occidentali  
 Nel caso delle lingue occidentali, se non si è certi delle lingue che verranno archiviate in una colonna o si prevede che verranno archiviate più lingue, provare a utilizzare il word breaker per la lingua più complessa che potrebbe essere archiviata nella colonna. È ad esempio possibile archiviare in una sola colonna contenuto nelle lingue inglese, spagnola e tedesca. Queste tre lingue occidentali sono basate su regole di suddivisione delle parole molto simili e delle tre il tedesco risulta essere la lingua più complessa. In questo caso, la soluzione ottimale potrebbe consistere nell'utilizzare il word breaker tedesco che dovrebbe essere in grado di elaborare correttamente il testo nelle lingue inglese e spagnola. Il word breaker inglese potrebbe invece non essere in grado di elaborare perfettamente il testo in tedesco per la presenza delle parole composte.  
  
 Si noti, tuttavia, che l'utilizzo del word breaker della lingua più complessa di una famiglia di lingue non garantisce un'indicizzazione perfetta di ogni lingua di tale famiglia. Potrebbero infatti verificarsi casi limite in cui il word breaker più complesso non è in grado di gestire correttamente il testo scritto in un'altra lingua.  
  
  
### <a name="non-western-languages"></a>Lingue non occidentali  
 Per motivi linguistici, la soluzione precedente non può essere applicata alle lingue non occidentali come il cinese, il giapponese, l'hindi e così via. Per queste lingue, considerare una delle soluzioni alternative seguenti:  
  
-   Per lingue di famiglie diverse  
  
     Se una colonna dovesse contenere testo in lingue radicalmente diverse, ad esempio spagnolo e giapponese, valutare la possibilità di archiviare tale contenuto in colonne diverse. In questo modo, sarebbe possibile utilizzare il word breaker specifico della lingua contenuta in ciascuna colonna. Se si sceglie questa soluzione e non si conosce la lingua da utilizzare in fase di query, potrebbe essere necessario eseguire la query in entrambe le colonne per essere sicuri che la query trovi la riga o il documento corretto.  
  
-   Contenuto binario (documenti di Microsoft Word)  
  
     Se il contenuto indicizzato è di tipo **binary** , il filtro della ricerca full-text che elabora il contenuto di testo prima di inviarlo al word breaker potrebbe rispettare specifici tag della lingua presenti nel file binario. In questo caso, durante l'indicizzazione il filtro genererà l'LCID corretto per un documento o una sezione di un documento. Il motore di ricerca full-text chiamerà quindi il word breaker per la lingua avente l'LCID specificato. È tuttavia consigliabile che al termine dell'indicizzazione di contenuto in più lingue venga verificato che non siano stati commessi errori.  
  
-   Contenuto di testo normale  
  
     Se il contenuto è testo normale, è possibile convertirlo nel tipo di dati **xml** e aggiungere tag che indichino la lingua corrispondente a ogni documento o sezione di documento specifica. Affinché questa soluzione funzioni, tuttavia, è necessario conoscere la lingua prima di procedere all'indicizzazione full-text.  
  
  
##  <a name="stemming"></a><a name="stemming"></a> Stemming  
 Quando si sceglie la lingua a livello di colonna è anche necessario prendere in considerazione lo stemming. Nell'ambito delle query full-text il termine*stemming* definisce il processo di ricerca di tutte le forme flessive di una parola di una determinata lingua. Quando si utilizza un word breaker generico per elaborare più lingue, il processo di stemming funziona solo per la lingua specificata per la colonna, non per le altre lingue presenti nella colonna. Ad esempio, gli stemmer del tedesco non funzionano per l'inglese o lo spagnolo e così via. Tutto questo potrebbe influire sulla chiamata a seconda della lingua scelta in fase di query.  
  
  
##  <a name="effect-of-column-type-on-full-text-search"></a><a name="type"></a> Effetto del tipo di colonna sulla ricerca full-text  
 Un'altra considerazione relativa alla scelta della lingua riguarda la modalità di rappresentazione dei dati. Ai dati non archiviati nella colonna **varbinary(max)** non vengono applicati filtri speciali. Il testo, al contrario, viene normalmente passato tramite il componente per l'esecuzione del word breaking così com'è.  
  
 I word breaker, inoltre, vengono progettati soprattutto per elaborare il testo scritto. Ne consegue che, se il testo include un tipo qualsiasi di markup (ad esempio HTML) le operazioni di indicizzazione e ricerca potrebbero non essere sufficientemente accurate dal punto di vista linguistico. In tal caso esistono due possibilità. Il metodo preferito consiste semplicemente nell'archiviare i dati di testo nella colonna **varbinary(max)** e indicare il tipo del documento per consentire l'applicazione del filtro. Se questa operazione non è possibile, valutare la possibilità di utilizzare il word breaker neutro ed eventualmente di aggiungere dati di markup, ad esempio "br" nel codice HTML, agli elenchi delle parole non significative.  
  
> [!NOTE]  
>  Lo stemming basato sulla lingua non viene eseguito se si specifica la lingua neutra.  
  
  
##  <a name="specifying-a-non-default-column-level-language-in-a-full-text-query"></a><a name="nondef"></a> Scelta di una lingua a livello di colonna non predefinita in una query full-text  
 Per impostazione predefinita, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la ricerca full-text analizza i termini delle query usando la lingua specificata per ogni colonna inclusa nella clausola full-text. Per modificare questo comportamento, specificare una lingua non predefinita in fase di query. Per le lingue supportate di cui sono state installate le risorse, è possibile usare la clausola *language_term* LANGUAGE di una query [CONTAINS](../../t-sql/queries/contains-transact-sql.md), [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md), [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)o [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) per specificare la lingua usata per l'esecuzione del word breaker, dello stemming, del thesaurus e delle parole non significative dei termini della query.  
  
  
## <a name="see-also"></a>Vedere anche  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [Configurazione e gestione di filtri per la ricerca](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)   
 [Configurazione e gestione di word breaker e stemmer per la ricerca](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  
