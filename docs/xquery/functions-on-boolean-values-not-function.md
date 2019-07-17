---
title: Funzione NOT (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- effective Boolean value [XQuery]
- fn:not function
- not function [XQuery]
- EBV
ms.assetid: 93dfc377-45f1-4384-9392-560d9331a915
author: rothja
ms.author: jroth
ms.openlocfilehash: 8711190a6d3cbae0c716f7f62af478b70b9473e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038910"
---
# <a name="functions-on-boolean-values---not-function"></a>Funzioni su valori booleani - not 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce TRUE se il valore booleano effettivo della *$arg* è false e restituisce FALSE se il valore booleano effettivo della *$arg* è true.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Una sequenza di elementi per i quali esiste un valore booleano effettivo.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo nel database AdventureWorks.  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>R. Utilizzo della funzione XQuery NOT () per trovare modelli di prodotti con descrizioni di catalogo non includono il \<specifiche > elemento.  
 La query seguente costruisce codice XML che contiene gli ID dei modelli di prodotto per i modelli di prodotti con descrizioni di catalogo non includono i <`Specifications`> elemento.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
       <Product   
           ProductModelID="{ sql:column("ProductModelID") }"  
        />  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications/*)]  '  
     ) = 0  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Poiché il documento utilizza gli spazi dei nomi, nell'esempio viene utilizzata l'istruzione WITH NAMESPACES. Un'altra opzione consiste nell'usare la **dichiarare lo spazio dei nomi** parola chiave nel [prologo XQuery](../xquery/modules-and-prologs-xquery-prolog.md) per definire il prefisso.  
  
-   La query genera quindi il codice XML che include il <`Product`> elemento e il relativo **ProductModelID** attributo.  
  
-   La clausola WHERE utilizza il [metodo exist () (tipo di dati XML)](../t-sql/xml/exist-method-xml-data-type.md) per filtrare le righe. Il **exist ()** metodo restituisce True se esistono \<ProductDescription > gli elementi che non hanno \<Specification > gli elementi figlio. Si noti l'uso del **NOT ()** (funzione).  
  
 Questo set di risultati è vuoto, perché ogni descrizione del catalogo prodotti sono inclusi il \<specifiche > elemento.  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. Utilizzo della funzione XQuery not() per recuperare i centri di lavorazione privi dell'attributo MachineHours  
 La query seguente viene specificata sulla colonna Instructions. Nella colonna sono archiviate le istruzioni di produzione dei modelli di prodotto.  
  
 Per un particolare modello di prodotto, la query recupera i centri di lavorazione che non specificano MachineHour, Vale a dire, l'attributo **MachineHours** non viene specificato per il \<Location > elemento.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in /AWMI:root/AWMI:Location[not(@MachineHours)]  
     return  
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ $i/@LaborHours }" >  
        </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7   
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Il **declarenamespace** nelle [prologo XQuery](../xquery/modules-and-prologs-xquery-prolog.md) definisce il prefisso dello spazio dei nomi di istruzioni di produzione di Adventure Works. Rappresenta lo stesso spazio dei nomi utilizzato nel documento di istruzioni di produzione.  
  
-   Nella query, il **non (@MachineHours)** predicato restituisce True se è presente alcun **MachineHours** attributo.  
  
 Questo è il risultato:  
  
```  
ProductModelID Result   
-------------- --------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Il **NOT ()** funzione supporta solo argomenti di tipo xs: Boolean o Node () * oppure la sequenza vuota.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
