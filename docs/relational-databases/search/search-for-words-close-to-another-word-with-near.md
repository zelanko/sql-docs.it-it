---
title: Cercare parole vicine a un'altra parola con NEAR | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
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
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0e94bdcf4770190d3d84986b511996213fac17f9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68702837"
---
# <a name="search-for-words-close-to-another-word-with-near"></a>Ricerca di parole vicine a un'altra parola con NEAR
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Per cercare parole o espressioni vicine, è possibile usare il *termine di prossimità* **NEAR** in un predicato [CONTAINS](../../t-sql/queries/contains-transact-sql.md) o in una funzione [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md). 
  
##  <a name="Custom_NEAR"></a> Panoramica di NEAR  
**NEAR** include le funzionalità seguenti:  
-   È possibile specificare il numero massimo di termini non di ricerca che separano il primo e l'ultimo termine di ricerca.

-   È possibile cercare parole o frasi in qualsiasi ordine o parole e frasi in un ordine specifico.
  
-   È possibile specificare il numero massimo di termini non di ricerca, oppure la *distanza massima*che separa il primo e l'ultimo termine di ricerca per formare una corrispondenza.  

-   Se si specifica il numero massimo di termini, è inoltre possibile specificare che nelle corrispondenze devono essere inclusi i termini di ricerca nell'ordine specificato.

 
 Per essere considerata una corrispondenza, una stringa di testo deve soddisfare i seguenti requisiti:  
  
-   Iniziare con uno dei termini di ricerca specificati e terminare con uno degli altri termini di ricerca specificati.  
  
-   Contenere tutti i termini di ricerca specificati.  
  
-   Il numero di termini non di ricerca, incluse le parole non significative, presenti tra i primo e l'ultimo termine di ricerca deve essere minore o uguale alla distanza massima, se specificata.  
  
## <a name="syntax-of-near"></a>Sintassi di NEAR
La sintassi di base di **NEAR** è la seguente:  

``` 
 NEAR (  
  
 {  
  
 *search_term* [ ,...*n* ]  
  
 |  
  
 (*search_term* [ ,...*n* ] ) [, <maximum_distance> [, <match_order> ] ]  
  
 }  
  
 )  
```

Per altre informazioni sulla sintassi, vedere [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md).  

## <a name="examples"></a>Esempi
### <a name="example-1"></a>Esempio 1
 È possibile, ad esempio, cercare 'John' entro due termini 'Smith', come segue:  
  
```sql
... CONTAINS(column_name, 'NEAR((John, Smith), 2)')
```  
  
 Esempi di stringhe corrispondenti sono "`John Jacob Smith`" e "`Smith, John`". La stringa "`John Jones knows Fred Smith`" include tre termini non di ricerca intermedi, pertanto non è una corrispondenza.  
  
 Per ottenere che i termini vengano trovati nell'ordine specificato, modificare il termine di prossimità di esempio in `NEAR((John, Smith),2, TRUE).` In questo modo viene effettuata la ricerca di "`John`" entro due termini "`Smith`", ma solo quando "`John`" precede "`Smith`". In una lingua con direzione di lettura da sinistra a destra, ad esempio la lingua inglese, un esempio di stringa corrispondente è il seguente: "`John Jacob Smith`".  
  
 Si noti che per le lingue con lettura da destra a sinistra, come l'arabo o l'ebraico, i termini specificati vengono applicati in ordine inverso dal motore di ricerca full-text. L'ordine di visualizzazione di parole specificate nelle lingue con scrittura da destra a sinistra viene inoltre invertito automaticamente da Esplora oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .   

### <a name="example-2"></a>Esempio 2
 Nell'esempio seguente viene effettuata la ricerca nella tabella `Production.Document` del database di esempio `AdventureWorks` di tutti i riepiloghi di documenti che contengono sia la parola "riflettore" che la parola "supporto".  
  
```sql
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
``` 
 
## <a name="how-maximum-distance-is-measured"></a>Modalità di misurazione della distanza massima  
 Una distanza massima specifica, ad esempio 10 o 25, determina il numero di termini non di ricerca, incluse le parole non significative, che possono essere presenti tra il primo e l'ultimo termine di ricerca in una determinata stringa. Ad esempio, `NEAR((dogs, cats, "hunting mice"), 3)` restituirà la riga seguente nella quale sono complessivamente presenti tre termini non di ricerca ("`enjoy`", "`but`" e "`avoid`"):  
  
 "`Cats` `enjoy` `hunting mice``, but avoid` `dogs``.`"  
  
 Lo stesso termine di prossimità non restituirà la riga seguente, perché la distanza massima viene superata dai quattro termini non di ricerca ("`enjoy`", "`but`", "`usually`" e "`avoid`"):  
  
 "`Cats` `enjoy` `hunting mice``, but usually avoid` `dogs``.`"  
  
## <a name="combine-near-with-other-terms"></a>Combinare NEAR con altri termini  
 È possibile combinare NEAR con altri termini. È possibile usare AND (&), OR (|) oppure AND NOT (&!) per combinare un termine di prossimità personalizzato con un altro termine di prossimità personalizzato, un termine semplice o un termine prefisso. Ad esempio:  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) OR *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND NOT *term3*')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) AND NEAR((*term3*, *term4*),2)')  
  
-   CONTAINS('NEAR((*term1*, *term2*),5) OR NEAR((*term3*, *term4*),2, TRUE)')  
  
 Ad esempio,  
  
```  
CONTAINS(column_name, 'NEAR((term1, term2), 5, TRUE) AND term3')  
```  
  
 Non è possibile combinare NEAR con un termine generazionale (ISABOUT ...) o un termine ponderato (FORMSOF ...).  
  
##  <a name="Additional_Considerations"></a> Altre informazioni sulle ricerche di prossimità  
   
-   Occorrenze di termini di ricerca sovrapposte  
  
     In tutte le ricerche per prossimità viene sempre effettuata la ricerca solo di occorrenze non sovrapposte. Le occorrenze di termini di ricerca sovrapposte non vengono mai considerate come corrispondenze. Si consideri, ad esempio, il termine di prossimità seguente che effettua la ricerca di "`A`" e "`AA`" in questo ordine con una distanza massima di due termini:  
  
    ```  
    CONTAINS(column_name, 'NEAR((A,AA), 2, TRUE)')
    ```  
  
     Le corrispondenze possibili sono "`AAA`", "`A.AA`" e "`A..AA`". Le righe che contengono solo "`AA`" non restituirebbero alcuna corrispondenza.  
  
    > [!NOTE]  
    >  È possibile specificare termini che si sovrappongono, ad esempio, `NEAR("mountain bike", "bike trails")` o `(NEAR(comfort*, comfortable), 5)`. In tal caso, tuttavia, aumenterebbe la complessità della query, aumentando di conseguenza le possibili permutazioni delle corrispondenze. Se si specifica un numero elevato di tali termini sovrapposti, è possibile che le risorse della query si esauriscano e che l'operazione abbia esito negativo. In tal caso, semplificare la query e riprovare.  
  
-   NEAR (indipendentemente dal fatto venga specificata o meno una distanza massima) indica la distanza logica anziché la distanza assoluta tra i termini. Ad esempio, i termini all'interno di espressioni o frasi diverse di un paragrafo vengono trattati come più lontani dei termini nella stessa espressione o frase, indipendentemente dalla loro prossimità effettiva, presupponendo che siano meno correlati. In modo analogo, i termini presenti in paragrafi diversi vengono trattati come ancora più lontani. Se una corrispondenza si estende fino alla fine di una frase, un paragrafo o un capitolo, il gap utilizzato per la classificazione per rango di un documento viene aumentato rispettivamente di 8, 128 o 1024.  
  
-   Impatto dei termini di prossimità sulla classificazione per rango tramite la funzione CONTAINSTABLE  
  
    Quando NEAR viene utilizzato nella funzione CONTAINSTABLE, il numero di riscontri presenti in un documento in rapporto alla relativa lunghezza, nonché alla distanza tra i primo e l'ultimo termine di ricerca in ognuno dei riscontri, influisce sulla classificazione per rango di ogni documento. Per un termine di prossimità generico, se i termini di ricerca corrispondenti sono separati da >50 termini logici, il rango restituito per un documento sarà pari a 0. Per un termine di prossimità personalizzato in cui non è specificato un intero come distanza massima, il rango restituito per un documento che contiene solo riscontri il cui gap è >100 termini logici sarà pari a 0. Per altre informazioni sulla classificazione per rango di ricerche per prossimità personalizzate, vedere [Limitare i risultati della ricerca con RANK](../../relational-databases/search/limit-search-results-with-rank.md).  
  
-   Opzione server **Transform Noise Words**  
  
     Il valore di **Transform Noise Words** influisce sul modo in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestisce le parole non significative, se vengono specificate nelle ricerche per prossimità. Per altre informazioni, vedere [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).   
  
## <a name="see-also"></a>Vedere anche  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Eseguire query con ricerca full-text](../../relational-databases/search/query-with-full-text-search.md)   
