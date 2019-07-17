---
title: StructureColumn (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7b6b436527aa36fb8f048a3b3c8fc55b970ef284
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065393"
---
# <a name="structurecolumn-dmx"></a>StructureColumn (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce il valore della colonna della struttura corrispondente al case specificato oppure il valore di tabella relativo a una tabella nidificata nel case specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
StructureColumn('structure column name')  
```  
  
## <a name="arguments"></a>Argomenti  
 nome-colonna-struttura.  
 Nome della colonna della struttura di data mining di un case o di una tabella nidificata.  
  
## <a name="result-type"></a>Tipo di risultato  
 Il tipo restituito dipende dal tipo della colonna a cui fa riferimento il \<nome colonna di struttura > parametro. Ad esempio, se la colonna della struttura di data mining a cui viene fatto riferimento contiene un valore scalare, la funzione restituisce un valore scalare.  
  
 Se la colonna della struttura di data mining alla quale viene fatto riferimento è una tabella nidificata, la funzione restituisce un valore di tabella. Il valore di tabella restituito può essere utilizzato nella clausola FROM di un'istruzione sub-SELECT.  
  
## <a name="remarks"></a>Note  
 Questa funzione è polimorfica e può essere utilizzata in qualunque posizione in un'istruzione che consente espressioni, comprese un elenco di espressioni SELECT, un'espressione di condizione WHERE e un'espressione ORDER BY.  
  
 Il nome della colonna nella struttura di data mining è un valore stringa e di conseguenza deve essere racchiuso tra virgolette singole: ad esempio, `StructureColumn('` **colonna 1**`')`. Nel caso in cui siano presenti più colonne con lo stesso nome, il nome è risolto nel contesto dell'istruzione SELECT che lo racchiude.  
  
 I risultati restituiti da una query tramite il **StructureColumn** funzione sono interessate dalla presenza di eventuali filtri nel modello. ovvero il filtro del modello controlla i case inclusi nel modello di data mining. Una query nella colonna della struttura può pertanto restituire solo i case utilizzati nel modello di data mining. Per un esempio di codice che illustra l'effetto dei filtri del modello di data mining sia in tabelle del case che in tabelle nidificate, vedere la sezione Esempi di questo argomento.  
  
 Per altre informazioni su come usare questa funzione in un'istruzione DMX SELECT, vedere [SELECT FROM &#60;modello&#62;. I casi &#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md) oppure [SELECT FROM &#60;struttura&#62;. CASI](../dmx/select-from-structure-cases.md).  
  
## <a name="error-messages"></a>messaggi di errore  
 Se l'utente non dispone di autorizzazioni drill-through sulla struttura di data mining padre, viene generato l'errore di sicurezza seguente:  
  
 Il ' % {utente /}' utente non dispone dell'autorizzazione per il drill-through nella struttura di data mining padre di ' % {model /}' modello di data mining.  
  
 Se il nome della colonna della struttura specificato non è valido, viene generato il messaggio di errore seguente:  
  
 Il ' % {structure-column-name /}' colonna della struttura di data mining non è stato trovato nel ' % {struttura /}' padre struttura di data mining nel contesto corrente (riga % {line /}, colonna % {colonna /}).  
  
## <a name="examples"></a>Esempi  
 Per questi esempi sarà utilizzata la struttura di data mining riportata di seguito. Si noti che la struttura di data mining contiene due colonne di tabelle nidificate, `Products` e `Hobbies`. La tabella nidificata nella colonna `Hobbies` contiene una singola colonna che viene utilizzata come chiave per la tabella nidificata. La tabella nidificata nella colonna `Products` è una tabella nidificata complessa con una colonna chiave e altre colonne utilizzate per l'input. Negli esempi seguenti viene illustrato come progettare una struttura di data mining per includere colonne diverse, anche se un modello potrebbe non utilizzare tutte le colonne. Alcune di queste colonne potrebbero non essere utili a livello di modello per la generalizzazione dei modelli, ma rivelarsi molto indicate per il drill-through.  
  
```  
CREATE MINING STRUCTURE [MyStructure]   
(  
CustomerName TEXT KEY,  
Occupation TEXT DISCRETE,  
Age LONG CONTINUOUS,  
MaritalStatus TEXT DISCRETE,  
Income LONG CONTINUOUS,  
Products  TABLE  
 (  
    ProductNameTEXT KEY,  
    Quantity LONG CONTINUOUS,  
    OnSale BOOLEAN  DISCRETE  
)  
 Hobbies  TABLE  
 (  
    Hobby KEY  
 ))  
```  
  
 Creare quindi un modello di data mining basato sulla struttura appena creata utilizzando il codice di esempio seguente:  
  
```  
ALTER MINING STRUCTURE [MyStructure] ADD MINING MODEL [MyModel] (  
CustomerName,  
Age,  
MaritalStatus,  
Income PREDICT,  
Products   
(  
ProductName  
) WITH FILTER(NOT OnSale)  
) USING Microsoft_Decision_Trees   
WITH FILTER(EXISTS (Products))  
```  
  
### <a name="sample-query-1-returning-a-column-from-the-mining-structure"></a>Esempio di Query 1: Restituzione di una colonna dalla struttura di Data Mining  
 Nella query di esempio seguente vengono restituite le colonne `CustomerName` e `Age`, definite come parte del modello di data mining. Tuttavia la query restituisce anche la colonna `Age`, che fa parte della struttura ma non è inclusa nel modello di data mining.  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation') FROM MyModel.CASES   
WHERE Age > 30  
```  
  
 Si noti che per limitare i case ai clienti di età superiore ai 30 anni il filtro delle righe viene applicato a livello del modello. Pertanto, questa espressione non restituisce case inclusi nei dati della struttura ma non utilizzati dal modello. Poiché la condizione di filtro utilizzata per creare il modello, `EXISTS (Products)`, limita i case solo ai clienti che hanno acquistato prodotti, nella struttura ci potrebbero essere case che non vengono restituiti dalla query.  
  
### <a name="sample-query-2-applying-a-filter-to-the-structure-column"></a>Esempio di Query 2: Applicare un filtro alla colonna della struttura  
 Nella query di esempio seguente, oltre alle colonne del modello `CustomerName` e `Age` e alla tabella nidificata `Products`, viene restituito il valore della colonna `Quantity` nella tabella nidificata che non fa parte del modello.  
  
```  
SELECT CustomerName, Age,  
(SELECT ProductName, StructureColumn('Quantity') FROM Products) FROM MA.CASES   
WHERE StructureColumn('Occupation') = 'Architect'  
```  
  
 Si noti che, in questo esempio viene applicato un filtro alla colonna della struttura per limitare i case ai clienti con occupazione 'Architect' (`WHERE StructureColumn('Occupation') = 'Architect'`). Poiché la condizione di filtro del modello viene sempre applicata ai case al momento della creazione del modello, vengono inclusi nei case del modello solo i case con almeno una riga risultante nella tabella `Products`. Vengono pertanto applicati sia il filtro sulla tabella nidificata `Products` che il filtro sul case `('Occupation')`.  
  
### <a name="sample-query-3-selecting-columns-from-a-nested-table"></a>Esempio di Query 3: Selezione di colonne da una tabella nidificata  
 Nella query di esempio seguente vengono restituiti i nomi dei clienti che sono stati utilizzati come case di training dal modello. Per ogni cliente, la query restituisce anche una tabella nidificata contenente i dettagli dell'acquisto. Anche se il modello include il `ProductName` colonna, il modello non utilizza il valore della `ProductName` colonna. Il modello di verifica solo se è stato acquistato il prodotto alle normali (`NOT``OnSale`) prezzo. Questa query non solo restituisce il nome del prodotto, ma anche la quantità acquistata che non è inclusa nel modello.  
  
```  
SELECT CustomerName,    
(SELECT ProductName, StructureColumn('Quantity')FROM Products)   
FROM MyModel.CASES  
```  
  
 Si noti che non è possibile restituire la colonna `ProductName` o `Quantity` se non è attivato il drill-through nel modello di data mining.  
  
### <a name="sample-query-4-filtering-on-and-returning-nested-table-columns"></a>Esempio di Query 4: Applicazione di filtri e restituzione di colonne della tabella nidificata  
 Nella query di esempio seguente vengono restituite le colonne della tabella nidificata e del case incluse nella struttura di data mining ma non nel modello. Sul modello è già applicato un filtro relativo alla presenza di prodotti `OnSale`, ma questa query aggiunge un filtro nella colonna della struttura di data mining, `Quantity`:  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation'),   
(SELECT ProductName, StructureColumn('Quantity') FROM Products)   
FROM MyModel.CASES   
WHERE EXISTS (SELECT * FROM Products WHERE StructureColumn('Quantity')>1)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Le funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
