---
title: Espressioni quantificate (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- universal quantifiers
- effective Boolean value [XQuery]
- quantified expressions [XQuery]
- XQuery, quantified expressions
- every expression [XQuery]
- existential quantifiers [XQuery]
- some expression [XQuery]
- EBV
- expressions [XQuery], quantifiers
ms.assetid: a3a75a6c-8f67-4923-8406-1ada546c817f
author: rothja
ms.author: jroth
ms.openlocfilehash: 1cdbff23d2158dec00b6b8d050d6a4a90341bd23
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946372"
---
# <a name="quantified-expressions-xquery"></a>Espressioni quantificate (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  I quantificatori esistenziali e universali specificano una semantica diversa per gli operatori booleani applicati a due sequenze, come illustrato nella tabella seguente.  
  
 *Quantificatore esistenziale*  
 Date due sequenze, se un elemento della prima sequenza ha una corrispondenza nella seconda sequenza, in base all'operatore di confronto utilizzato, viene restituito il valore True.  
  
 *Quantificatore universale*  
 Date due sequenze, se tutti gli elementi della prima sequenza hanno una corrispondenza nella seconda sequenza viene restituito il valore True.  
  
 XQuery supporta le espressioni quantificate nel formato seguente:  
  
```  
( some | every ) <variable> in <Expression> (,...) satisfies <Expression>  
```  
  
 È possibile utilizzare queste espressioni in una query per applicare esplicitamente la quantificazione esistenziale o universale a un'espressione su una o più sequenze. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], l'espressione nella clausola `satisfies` deve generare una sequenza di nodi, una sequenza vuota oppure un valore booleano. Il valore booleano effettivo del risultato dell'espressione verrà utilizzato nella quantificazione. La quantificazione esistenziale che usa **alcuni** restituirà true se almeno uno dei valori associati dal quantificatore ha un risultato true nell'espressione di soddisfazione. La quantificazione universale che usa **ogni** deve avere true per tutti i valori associati dal quantificatore.  
  
 Ad esempio, la query seguente controlla ogni \<posizione> elemento per verificare se dispone di un attributo LocationID.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        if (every $WC in //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID)  
        then  
             <Result>All work centers have workcenterLocation ID</Result>  
         else  
             <Result>Not all work centers have workcenterLocation ID</Result>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Poiché LocationID è un attributo obbligatorio dell'elemento \<location>, viene visualizzato il risultato previsto:  
  
```  
<Result>All work centers have Location ID</Result>   
```  
  
 Anziché utilizzare il [metodo query ()](../t-sql/xml/query-method-xml-data-type.md), è possibile utilizzare il [metodo value ()](../t-sql/xml/value-method-xml-data-type.md) per restituire il risultato al mondo relazionale, come illustrato nella query seguente. La query restituisce True se tutti i centri di lavorazione includono attributi LocationID. In caso contrario, la funzione restituisce False.  
  
```  
SELECT Instructions.value('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        every $WC in  //AWMI:root/AWMI:Location   
            satisfies $WC/@LocationID',   
  'nvarchar(10)') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 La query seguente verifica se una delle immagini del prodotto è di piccole dimensioni. Nel codice XML del catalogo prodotti sono archiviate varie angolazioni per ogni dimensione di immagine dei prodotti. Può essere necessario verificare che il codice XML del catalogo prodotti includa almeno un'immagine di piccole dimensioni. La query seguente esegue questa operazione:  
  
```  
SELECT ProductModelID, CatalogDescription.value('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     some $F in /PD:ProductDescription/PD:Picture  
        satisfies $F/PD:Size="small"', 'nvarchar(20)') as SmallPicturesStored  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Risultato parziale:  
  
```  
ProductModelID SmallPicturesStored   
-------------- --------------------  
19             true        
```  
  
## <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   L'asserzione del tipo non è supportata come parte dell'associazione della variabile nelle espressioni quantificate.  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni XQuery](../xquery/xquery-expressions.md)  
  
  
