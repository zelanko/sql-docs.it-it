---
title: Funzione not (XQuery) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038910"
---
# <a name="functions-on-boolean-values---not-function"></a>Funzioni su valori booleani - not 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce TRUE se il valore booleano effettivo di *$arg* è false e restituisce false se il valore booleano effettivo di *$arg* è true.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Una sequenza di elementi per i quali esiste un valore booleano effettivo.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse colonne di tipo **XML** nel database AdventureWorks.  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>A. Utilizzo della funzione XQuery not () per individuare i modelli di prodotto le cui descrizioni del catalogo \<non includono le specifiche> elemento.  
 La query seguente costruisce codice XML contenente gli ID del modello di prodotto per i quali le descrizioni del catalogo non `Specifications` includono l'elemento <>.  
  
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
  
-   Poiché il documento utilizza gli spazi dei nomi, nell'esempio viene utilizzata l'istruzione WITH NAMESPACES. Un'altra opzione consiste nell'utilizzare la parola chiave **declare namespace** nel [prologo XQuery](../xquery/modules-and-prologs-xquery-prolog.md) per definire il prefisso.  
  
-   La query costruisce quindi il codice XML che include l' `Product` elemento <> e il relativo attributo **ProductModelID** .  
  
-   La clausola WHERE usa il [metodo exist () (tipo di dati XML)](../t-sql/xml/exist-method-xml-data-type.md) per filtrare le righe. Il metodo **exist ()** restituisce true se sono \<presenti elementi ProductDescription> che non dispongono \<di specifiche> elementi figlio. Si noti l'uso della funzione **Not ()** .  
  
 Questo set di risultati è vuoto, perché ogni descrizione del catalogo del modello \<di prodotto include le specifiche> elemento.  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. Utilizzo della funzione XQuery not() per recuperare i centri di lavorazione privi dell'attributo MachineHours  
 La query seguente viene specificata sulla colonna Instructions. Nella colonna sono archiviate le istruzioni di produzione dei modelli di prodotto.  
  
 Per un particolare modello di prodotto, la query recupera i centri di lavorazione che non specificano MachineHour, Ovvero, l'attributo **MachineHours** non è specificato per il \<percorso> elemento.  
  
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
  
-   Il **declarenamespace** nel [prologo XQuery](../xquery/modules-and-prologs-xquery-prolog.md) definisce il prefisso dello spazio dei nomi delle istruzioni di produzione di Adventure Works. Rappresenta lo stesso spazio dei nomi utilizzato nel documento di istruzioni di produzione.  
  
-   Nella query il predicato **Not@MachineHours()** restituisce true se non è presente alcun attributo **MachineHours** .  
  
 Risultato:  
  
```  
ProductModelID Result   
-------------- --------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   La funzione **Not ()** supporta solo argomenti di tipo xs: Boolean o node () *, oppure la sequenza vuota.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
