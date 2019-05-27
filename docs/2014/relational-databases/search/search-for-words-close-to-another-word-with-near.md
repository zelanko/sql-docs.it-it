---
title: Cercare parole vicine a un'altra parola con NEAR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- word searches [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- proximity searches [full-text search]
- full-text search [SQL Server], proximity searches
- full-text queries [SQL Server], proximity
- queries [full-text search], proximity
ms.assetid: 87520646-4865-49ae-8790-f766b80a41f3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fadff7e68404ffae528cb4630e1f6c4b8156ccc0
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011071"
---
# <a name="search-for-words-close-to-another-word-with-near"></a>Ricerca di parole vicine a un'altra parola con NEAR
  Per cercare parole o frasi vicine, è possibile usare un termine di prossimità (NEAR) in un predicato [CONTAINS](/sql/t-sql/queries/contains-transact-sql) o in una funzione [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql). È inoltre possibile specificare il numero massimo di termini non di ricerca che separano il primo e l'ultimo termine di ricerca. È inoltre possibile cercare parole o frasi in qualsiasi ordine o parole e frasi nell'ordine in cui sono state specificate. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] supporta sia la precedente [termine di prossimità generico](#Generic_NEAR), che è ora deprecato e il [termine di prossimità personalizzato](#Custom_NEAR), che è una novità [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
##  <a name="Custom_NEAR"></a> Il termine di prossimità personalizzato  
 Con il termine di prossimità personalizzato vengono introdotte le seguenti nuove funzionalità:  
  
-   È possibile specificare il numero massimo di termini non di ricerca, oppure la *distanza massima*che separa il primo e l'ultimo termine di ricerca per formare una corrispondenza.  
  
-   Se si specifica il numero massimo di termini, è inoltre possibile specificare che nelle corrispondenze devono essere inclusi i termini di ricerca nell'ordine specificato.  
  
 Per essere considerata una corrispondenza, una stringa di testo deve soddisfare i seguenti requisiti:  
  
-   Iniziare con uno dei termini di ricerca specificati e terminare con uno degli altri termini di ricerca specificati.  
  
-   Contenere tutti i termini di ricerca specificati.  
  
-   Il numero di termini non di ricerca, incluse le parole non significative, presenti tra i primo e l'ultimo termine di ricerca deve essere minore o uguale alla distanza massima, se specificato.  
  
 La sintassi di base è la seguente:  
  
 NEAR (  
  
 {  
  
 *search_term* [ ,...*n* ]  
  
 |  
  
 (*search_term* [ ,...*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
  
> [!NOTE]  
>  Per altre informazioni sulla sintassi di <custom_proximity_term>, vedere [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql).  
  
 È possibile, ad esempio, cercare 'John' entro due termini 'Smith', come segue:  
  
```  
CONTAINS(column_name, 'NEAR((John, Smith), 2)')  
```  
  
 Esempi di stringhe corrispondenti sono "`John Jacob Smith`" e "`Smith, John`". La stringa "`John Jones knows Fred Smith`" include tre termini non di ricerca intermedi, pertanto non è una corrispondenza.  
  
 Per ottenere che i termini vengano trovati nell'ordine specificato, modificare il termine di prossimità di esempio in `NEAR((John, Smith),2, TRUE).` In questo modo viene effettuata la ricerca di "`John`" entro due termini "`Smith`", ma solo quando "`John`" precede "`Smith`". In una lingua con direzione di lettura da sinistra a destra, ad esempio la lingua inglese, un esempio di stringa corrispondente è il seguente: "`John Jacob Smith`".  
  
 Si noti che per le lingue con lettura da destra a sinistra, come l'arabo o l'ebraico, i termini specificati vengono applicati in ordine inverso dal motore di ricerca full-text. L'ordine di visualizzazione di parole specificate nelle lingue con scrittura da destra a sinistra viene inoltre invertito automaticamente da Esplora oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
> [!NOTE]  
>  Per altre informazioni, vedere "[Considerazioni aggiuntive per le ricerche per prossimità](#Additional_Considerations)" più avanti in questo argomento.  
  
### <a name="how-maximum-distance-is-measured"></a>Modalità di misurazione della distanza massima  
 Una distanza massima specifica, ad esempio 10 o 25, determina il numero di termini non di ricerca, incluse le parole non significative, che possono essere presenti tra il primo e l'ultimo termine di ricerca in una determinata stringa. Ad esempio, `NEAR((dogs, cats, "hunting mice"), 3)` restituirà la riga seguente nella quale sono complessivamente presenti tre termini non di ricerca ("`enjoy`", "`but`" e "`avoid`"):  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 Lo stesso termine di prossimità non restituirà la riga seguente, perché la distanza massima viene superata dai quattro termini non di ricerca ("`enjoy`", "`but`", "`usually`" e "`avoid`"):  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
### <a name="combining-a-custom-proximity-term-with-other-terms"></a>Combinazione di un termine di prossimità personalizzato con altri termini  
 È possibile combinare un termine di prossimità personalizzato con alcuni altri termini. È possibile usare AND (&), OR (|) oppure AND NOT (&!) per combinare un termine di prossimità personalizzato con un altro termine di prossimità personalizzato, un termine semplice o un termine prefisso. Ad esempio:   
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) AND NEAR((*term3*,*term4*),2)')  
  
-   CONTAINS('NEAR((*term1*,*term2*),5) OR NEAR((*term3*,*term4*),2, TRUE)')  
  
 Ad esempio,  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 Non è possibile combinare un termine di prossimità personalizzato con un termine di prossimità generico (*term1* NEAR *term2*), un termine generazionale (ISABOUT...) o un termine ponderato (FORMSOF...).  
  
### <a name="example-using-the-custom-proximity-term"></a>Esempio: Utilizzo del termine di prossimità personalizzato  
 Nell'esempio seguente viene effettuata la ricerca nella tabella `Production.Document` del database di esempio `AdventureWorks2012` di tutti i riepiloghi di documenti che contengono sia la parola "riflettore" che la parola "supporto".  
  
```  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  

  
##  <a name="Additional_Considerations"></a> Considerazioni aggiuntive per ricerche per prossimità  
 In questa sezione vengono illustrate alcune considerazioni riguardanti le ricerche per prossimità sia generiche che personalizzate:  
  
-   Occorrenze di termini di ricerca sovrapposte  
  
     In tutte le ricerche per prossimità viene sempre effettuata la ricerca solo di occorrenze non sovrapposte. Le occorrenze di termini di ricerca sovrapposte non vengono mai considerate come corrispondenze. Si consideri, ad esempio, il termine di prossimità seguente che effettua la ricerca di "`A`" e "`AA`" in questo ordine con una distanza massima di due termini:  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA),2, TRUE')  
    ```  
  
     Le corrispondenze possibili sono "`AAA`", "`A.AA`" e "`A..AA`". Le righe che contengono solo "`AA`" non restituirebbero alcuna corrispondenza.  
  
    > [!NOTE]  
    >  È possibile specificare termini che si sovrappongono, ad esempio, `NEAR("mountain bike", "bike trails")` o `(NEAR(comfort*, comfortable), 5)`. In tal caso, tuttavia, aumenterebbe la complessità della query, aumentando di conseguenza le possibili permutazioni delle corrispondenze. Se si specifica un numero elevato di tali termini sovrapposti, è possibile che le risorse della query si esauriscano e che l'operazione abbia esito negativo. In tal caso, semplificare la query e riprovare.  
  
-   Sia il termine generico NEAR che il termine personalizzato NEAR (indipendentemente dal fatto venga specificata o meno una distanza massima) indicano la distanza logica anziché la distanza assoluta tra i termini. Ad esempio, i termini all'interno di espressioni o frasi diverse di un paragrafo vengono trattati come più lontani dei termini nella stessa espressione o frase, indipendentemente dalla loro prossimità effettiva, presupponendo che siano meno correlati. In modo analogo, i termini presenti in paragrafi diversi vengono trattati come ancora più lontani. Se una corrispondenza si estende fino alla fine di una frase, un paragrafo o un capitolo, il gap utilizzato per la classificazione per rango di un documento viene aumentato rispettivamente di 8, 128 o 1024.  
  
-   Impatto dei termini di prossimità sulla classificazione per rango tramite la funzione CONTAINSTABLE  
  
     Quando NEAR viene utilizzato nella funzione CONTAINSTABLE, il numero di riscontri presenti in un documento in rapporto alla relativa lunghezza, nonché alla distanza tra i primo e l'ultimo termine di ricerca in ognuno dei riscontri, influisce sulla classificazione per rango di ogni documento. Per un termine di prossimità generico, se i termini di ricerca corrispondenti sono separati da >50 termini logici, il rango restituito per un documento sarà pari a 0. Per un termine di prossimità personalizzato in cui non è specificato un intero come distanza massima, il rango restituito per un documento che contiene solo riscontri il cui gap è >100 termini logici sarà pari a 0. Per altre informazioni sulla classificazione per rango di ricerche per prossimità personalizzate, vedere [Limitare i risultati della ricerca con RANK](limit-search-results-with-rank.md).  
  
-   Opzione server **Transform Noise Words**  
  
     Il valore di **Transform Noise Words** influisce sul modo in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestisce le parole non significative, se vengono specificate nelle ricerche per prossimità. Per altre informazioni, vedere [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).  
  

  
##  <a name="Generic_NEAR"></a> Il termine di prossimità generico deprecato  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] È consigliabile usare la [termine di prossimità personalizzato](#Custom_NEAR).  
  
 Un termine di prossimità generico indica che i termini di ricerca specificati devono essere tutti presenti in un documento perché venga restituita una corrispondenza, indipendentemente dal numero di termini non di ricerca, ovvero la *distanza*, tra i termini di ricerca. La sintassi di base è la seguente:  
  
 { *search_term* { NEAR | ~ } *search_term* } [ ,...*n* ]  
  
 Negli esempi seguenti le parole 'fox' e 'chicken', ad esempio, devono essere entrambe presenti, indipendentemente dall'ordine, per produrre una corrispondenza:  
  
-   `CONTAINS(column_name, 'fox NEAR chicken')`  
  
-   `CONTAINSTABLE(table_name, column_name, 'fox ~ chicken')`  
  
> [!NOTE]  
>  Per informazioni sulla sintassi di <generic_proximity_term>, vedere [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql).  
  
 Per altre informazioni, vedere "[Considerazioni aggiuntive per le ricerche per prossimità](#Additional_Considerations)" più avanti in questo argomento.  
  
### <a name="combining-a-generic-proximity-term-with-other-terms"></a>Combinazione di un termine di prossimità generico con altri termini  
 È possibile usare AND (&), OR (|) oppure AND NOT (&!) per combinare un termine di prossimità generico con un altro termine di prossimità generico, un termine semplice o un termine prefisso. Ad esempio:   
  
```  
CONTAINSTABLE (Production.ProductDescription,  
   Description,   
   '(light NEAR aluminum) OR  
   (lightweight NEAR aluminum)'  
)  
```  
  
 È possibile combinare un termine di prossimità generico con un termine di prossimità personalizzato, ad esempio `NEAR((term1,term2),5)`, un termine ponderato (ISABOUT...) o un termine generazionale (FORMSOF...).  
  
### <a name="example-using-the-generic-proximity-term"></a>Esempio: Utilizzo del termine di prossimità generico  
 Nell'esempio seguente viene utilizzato il termine di prossimità generico per cercare la parola "reflector" nello stesso documento che contiene la parola "bracket".  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable INNER JOIN  
  CONTAINSTABLE(Production.Document, Document,  
  '(reflector NEAR bracket)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
 Si noti che invertendo i termini in CONTAINSTABLE si ottiene lo stesso risultato:  
  
```  
CONTAINSTABLE(Production.Document, Document, '(bracket NEAR reflector)' ) AS KEY_TBL  
```  
  
 È possibile ottenere lo stesso risultato sostituendo la parola chiave NEAR con una tilde (~):  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket)' ) AS KEY_TBL  
```  
  
 Nelle condizioni di ricerca è possibile includere più di due parole o frasi, ad esempio:  
  
```  
CONTAINSTABLE(Production.Document, Document, '(reflector ~ bracket ~ installation)' ) AS KEY_TBL  
```  
  
 Ciò significa che la parola "riflettore" deve trovarsi nello stesso documento della parola "supporto" e "supporto" deve trovarsi nello stesso documento della parola "installazione".  
  

  
## <a name="see-also"></a>Vedere anche  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [Eseguire query con ricerca full-text](query-with-full-text-search.md)   
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)  
  
  
