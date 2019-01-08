---
title: Esempi e sintassi del filtro del modello (Analysis Services - Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ae34f06997d1647f6345c0cf77494aa8688a8616
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52393547"
---
# <a name="model-filter-syntax-and-examples-analysis-services---data-mining"></a>Sintassi ed esempi di filtri dei modelli (Analysis Services – Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In questa sezione vengono fornite informazioni dettagliate sulla sintassi dei filtri dei modelli, insieme alle espressioni di esempio.  
  
 [Sintassi del filtro](#bkmk_Syntax)  
  
 [Filtri sugli attributi del case](#bkmk_Ex1)  
  
 [Filtri sugli attributi della tabella nidificata](#bkmk_Ex2)  
  
 [Filtri su più attributi della tabella nidificata](#bkmk_Ex3)  
  
 [Filtri sugli attributi mancanti nella tabella nidificata](#bkmk_Ex4)  
  
 [Filtri su più valori della tabella nidificata](#bkmk_Ex5)  
  
 [Filtri su attributi ed EXISTS della tabella nidificata](#bkmk_Ex6)  
  
 [Combinazioni di filtri](#bkmk_Ex7)  
  
 [Filtri sulle date](#bkmk_Ex8)  
  
##  <a name="bkmk_Syntax"></a> Filter Syntax  
 Le espressioni di filtro in genere sono equivalenti al contenuto di una clausola WHERE. È possibile connettere più condizioni usando gli operatori logici **AND**, **OR**e **NOT**.  
  
 Nelle tabelle annidate, è anche possibile usare gli operatori **EXISTS** e **NOT EXISTS** . Una condizione **EXISTS** restituisce **true** se la sottoquery restituisce almeno una riga. Ciò risulta utile nei case in cui si desidera limitare il modello ai case che contengono un determinato valore nella tabella nidificata: ad esempio, i clienti che hanno acquistato almeno una volta un articolo.  
  
 Una condizione **NOT EXISTS** restituisce **true** se la condizione specificata nella sottoquery non esiste. Ad esempio, quando si desidera limitare il modello ai clienti che non hanno mai acquistato un determinato articolo.  
  
 La sintassi generale è la seguente:  
  
```  
<filter>::=<predicate list>  | ( <predicate list> )  
<predicate list>::= <predicate> | [<logical_operator> <predicate list>]   
<logical_operator::= AND| OR  
<predicate>::= NOT <predicate>|( <predicate> ) <avPredicate> | <nestedTablePredicate> | ( <predicate> )   
<avPredicate>::= <columnName> <operator> <scalar> | <columnName> IS [NOT] NULL  
<operator>::= = | != | <> | > | >= | < | <=  
<nestedTablePredicate>::= EXISTS (<subquery>)  
<subquery>::=SELECT * FROM <columnName>[ WHERE  <predicate list> ]  
```  
  
 *filter*  
 Contiene uno o più predicati, connessi da operatori logici.  
  
 *elenco predicati*  
 Una o più espressioni di filtro valide, separate da operatori logici.  
  
 *columnName*  
 Nome della colonna della struttura di data mining.  
  
 operatore logico  
 **AND**, **OR**, **NOT**  
  
 *avPredicate*  
 Espressione del filtro che può essere applicata solo a una colonna scalare della struttura di data mining. Un'espressione *avPredicate* può essere usata sia nei filtri dei modelli sia nei filtri della tabella annidata.  
  
 Un'espressione che utilizza alcuni degli operatori seguenti può essere applicata solo a una colonna continua. :  
  
-   **\<** (minore di)  
  
-   **>** (maggiore di)  
  
-   **>=** (maggiore o uguale a)  
  
-   **\<=** (minore o uguale a)  
  
> [!NOTE]  
>  Indipendentemente dal tipo di dati, questi operatori non possono essere applicati a una colonna di tipo **Discreta**, **Discretizzata**o **Chiave**.  
  
 Un'espressione che utilizza alcuni degli operatori seguenti può essere applicata a una colonna continua, discreta, discretizzata o chiave:  
  
-   **=** (uguale a)  
  
-   **!=** (diverso da)  
  
-   **È NULL**  
  
 Se l'argomento *avPredicate*si applica a una colonna discretizzata, il valore usato nel filtro può essere qualsiasi valore in un bucket specifico.  
  
 In altre parole, la condizione non viene definita come `AgeDisc = '25-35'`, ma viene invece calcolata e viene quindi usato un valore dall'intervallo.  
  
 Esempio:  `AgeDisc = 27`  indica qualsiasi valore nello stesso intervallo di 27, in questo caso 25-35.  
  
 *nestedTablePredicate*  
 Espressione di filtro applicabile a una tabella nidificata. Può essere utilizzata solo nei filtri dei modelli.  
  
 L'argomento della sottoquery dell'argomento, *nestedTablePredicate*, può essere applicato solo a una colonna della struttura di data mining della tabella  
  
 Sottoquery  
 Istruzione SELECT seguita da un predicato valido o da un elenco di predicati.  
  
 Tutti i predicati devono corrispondere al tipo descritto in *avPredicates*. Inoltre, i predicati possono fare riferimento solo a colonne incluse nella tabella annidata attuale, identificata dall'argomento *columnName*.  
  
### <a name="limitations-on-filter-syntax"></a>Limitazioni della sintassi del filtro  
 Ai filtri si applicano le seguenti restrizioni:  
  
-   Un filtro può contenere solo predicati semplici. Questi includono operatori matematici, scalari e nomi delle colonne.  
  
-   Le funzioni definite dall'utente non sono supportate nella sintassi del filtro.  
  
-   Gli operatori non booleani, come i segni più o meno, non sono supportati nella sintassi del filtro.  
  
## <a name="examples-of-filters"></a>Esempi di filtri  
 Negli esempi seguenti viene illustrato l'utilizzo di filtri applicati a un modello di data mining. Se si crea l'espressione di filtro usando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], nella finestra **Proprietà** e nel riquadro **Espressione** della finestra di dialogo del filtro viene visualizzata solo la stringa presente dopo le parole chiave WITH FILTER. La definizione della struttura di data mining viene inclusa per semplificare e comprendere il tipo di colonna e l'utilizzo.  
  
###  <a name="bkmk_Ex1"></a> Esempio 1: Applicazione di filtri a livello del Case tipico  
 In questo esempio viene mostrato un semplice filtro che limita i case utilizzati nel modello ai clienti la cui occupazione è architetto e la cui età è superiore a 30 anni.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_1  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH FILTER (Age > 30 AND Occupation='Architect')  
```  
  
  
###  <a name="bkmk_Ex2"></a> Esempio 2: Applicazione di filtri a livello del case utilizzando gli attributi delle tabelle nidificate  
 Se la struttura di data mining contiene tabelle nidificate, è possibile filtrare in base all'esistenza di un valore in una tabella nidificata o in base alle righe della tabella nidificata che contengono un valore specifico. In questo esempio i case utilizzati per il modello vengono limitati ai clienti di età superiore ai 30 anni che hanno effettuato almeno un acquisto che include latte.  
  
 Come mostrato nell'esempio, non è necessario che il filtro utilizzi solo colonne incluse nel modello. La tabella annidata **Prodotti** fa parte della struttura di data mining, ma non è inclusa nel modello di data mining. Tuttavia, è ancora possibile filtrare in base a valori e attributi nella tabella nidificata. Per visualizzare i dettagli di questi case, è necessario attivare il drill-through.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_2  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH DRILLTHROUGH,   
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName='Milk')  
)  
```  
  
  
###  <a name="bkmk_Ex3"></a> Esempio 3: Applicazione di filtri a livello del case su più attributi della tabella nidificata  
 In questo esempio viene mostrato un filtro in tre parti: una condizione viene applicata alla tabella del case, un'altra a un attributo nella tabella nidificata e un'altra a un valore specifico in una delle colonne della tabella nidificata.  
  
 La prima condizione nel filtro, `Age > 30`, si applica a una colonna nella tabella del case. Le altre condizioni vengono applicate alla tabella nidificata.  
  
 La seconda condizione, `EXISTS (SELECT * FROM Products WHERE ProductName='Milk'`, verifica la presenza di almeno un acquisto nella tabella annidata che include il latte. La terza condizione, `Quantity>=2`, indica che il cliente deve aver acquistato almeno due unità di latte in una singola transazione.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_3  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
)  
)  
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName='Milk'  AND Quantity >= 2)   
)  
```  
  
  
###  <a name="bkmk_Ex4"></a> Esempio 4: Applicazione di filtri a livello del case in assenza di attributi della tabella nidificata  
 In questo esempio viene illustrata la limitazione dei case ai clienti che non ha acquistato un articolo specifico, filtrando in base all'assenza di un attributo nella tabella nidificata. In questo esempio, viene eseguito il training del modello utilizzando i clienti di età superiore ai 30 anni che non hanno mai comprato latte.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_4  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName  
)  
)  
FILTER (Age > 30 AND NOT EXISTS (SELECT * FROM Products WHERE ProductName='Milk') )  
```  
  
  
###  <a name="bkmk_Ex5"></a> Esempio 5: Applicazione di filtri su più valori di tabella nidificata  
 Lo scopo dell'esempio è mostrare l'applicazione del filtro sulla tabella nidificata. Il filtro della tabella nidificata viene applicato dopo il filtro del case e si limita solo alle righe della tabella nidificata.  
  
 Questo modello può contenere più case con tabelle nidificate vuote perché EXISTS non è specificato.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_5  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName='Milk' OR ProductName='bottled water')  
)  
WITH DRILLTHROUGH  
```  
  
  
###  <a name="bkmk_Ex6"></a> Esempio 6: Applicazione di filtri su attributi delle tabelle nidificate e alla clausola EXISTS  
 In questo esempio, il filtro nella tabella nidificata limita le righe a quelle che contengono latte o acqua imbottigliata. Quindi, i case nel modello vengono limitati tramite un'istruzione **EXISTS** . Ciò assicura che la tabella nidificata non è vuota.  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_6  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName='Milk' OR ProductName='bottled water')  
)  
FILTER (EXISTS (Products))  
```  
  
  
###  <a name="bkmk_Ex7"></a> Esempio 7: Combinazioni di filtri complessi  
 Lo scenario per questo modello è simile a quello dell'esempio 4, ma è molto più complesso. La tabella annidata **ProductsOnSale**possiede la condizione del filtro `(OnSale)` , pertanto il valore di **OnSale** deve essere **true** per il prodotto elencato in **ProductName**. In questo caso, **OnSale** è una colonna della struttura.  
  
 La seconda parte del filtro, per **ProductsNotOnSale**, ripete questa sintassi, ma applica il filtro in base ai prodotti per i quali il valore di **OnSale** è **not true**`(!OnSale)`.  
  
 Infine, le condizioni vengono combinate e viene aggiunta un'ulteriore restrizione alla tabella del case. Il risultato è la stima degli acquisti di prodotti nell'elenco **ProductsNotOnSale** , in base ai case inclusi nell'elenco **ProductsOnSale** , per tutti i clienti di età superiore ai 25 anni.  
  
 `ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_7`  
  
 `(`  
  
 `CustomerId,`  
  
 `Age,`  
  
 `Occupation,`  
  
 `MaritalStatus,`  
  
 `ProductsOnSale`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(OnSale),`  
  
 `ProductsNotOnSale PREDICT ONLY`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(!OnSale)`  
  
 `)`  
  
 `WITH DRILLTHROUGH,`  
  
 `FILTER (EXISTS (ProductsOnSale) AND EXISTS(ProductsNotOnSale) AND Age > 25)`  
  
  
###  <a name="bkmk_Ex8"></a> Esempio 8: Filtri sulle date  
 È possibile filtrare le colonne di input in base alle date, come per qualsiasi altro tipo di dati. Le date contenute in una colonna di tipo data/ora sono valori continui; è quindi possibile specificare un intervallo di date utilizzando operatori quali maggiore di (>) o minore di (<). Se l'origine dati non rappresenta le date come tipo di dati Continuous, ma come valori discreti o di testo, non sarà possibile filtrare in base a un intervallo di date, ma sarà necessario specificare singoli valori discreti.  
  
 Tuttavia, non è possibile creare un filtro sulla colonna delle date in un modello Time Series se la colonna delle date utilizzata per il filtro è anche la colonna chiave per il modello. Ciò accade poiché nei modelli Time Series e Sequence Clustering la colonna delle date potrebbe essere gestita come tipo **KeyTime** o **KeySequence**.  
  
 Quando è necessario applicare un filtro alle date continue in un modello Time Series, è possibile creare una copia della colonna nella struttura di data mining e filtrare il modello nella nuova colonna.  
  
 L'espressione seguente, ad esempio, rappresenta un filtro applicato a una colonna delle date di tipo **continue** aggiunta al modello Forecasting.  
  
 `=[DateCopy] > '12:31:2003:00:00:00'`  
  
> [!NOTE]  
>  L'aggiunta di una qualsiasi colonna al modello può influire sui risultati. Pertanto, se non si desidera che la colonna venga utilizzata nel calcolo della serie, sarà necessario aggiungere la colonna solo alla struttura di data mining e non al modello. È anche possibile impostare il flag del modello della colonna su **PredictOnly** o **Ignore**. Per altre informazioni, vedere [Flag di modellazione &#40;data mining&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md).  
  
 Per altri tipi di modello, è possibile utilizzare le date come criteri di input o criteri di filtro come si farebbe per qualsiasi altra colonna. Tuttavia, se è necessario usare un livello di granularità specifico non supportato da un tipo di dati **continuo** , sarà possibile creare un valore derivato nell'origine dati usando espressioni per estrarre l'unità da usare per filtri e analisi.  
  
> [!WARNING]  
>  Quando si specificano le date come criteri di filtro, è necessario usare il formato seguente, indipendentemente dal formato di data del sistema operativo attualmente in uso: `mm/dd/yyyy`. Qualsiasi altro formato restituirà un errore.  
  
 Se, ad esempio, si desidera filtrare i risultati del call center in modo da visualizzare solo i fine settimana, è possibile creare un'espressione nella vista origine dati che estragga il nome del giorno della settimana per ciascuna data e utilizzare quindi il valore del nome del giorno della settimana come input o come un valore discreto per i filtri. È sufficiente ricordare che la ripetizione dei valori può influire sul modello ed è quindi necessario utilizzare solo una delle colonne, non la colonna delle date insieme al valore derivato.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Filtri per i modelli di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [Test e convalida &#40;Data mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
