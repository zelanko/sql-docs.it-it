---
title: substring-funzione (XQuery) | Microsoft Docs
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
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
author: rothja
ms.author: jroth
ms.openlocfilehash: 2188cff20411fe90d4858763f65cff7f6fe9c9d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004647"
---
# <a name="functions-on-string-values---substring"></a>Funzioni su valori stringa - substring
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce parte del valore del *$sourceString*, iniziando in corrispondenza della posizione indicata dal valore di *$startingLoc,* e continua per il numero di caratteri indicato dal valore di *$ lunghezza*.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>Argomenti  
 *$sourceString*  
 Stringa di origine.  
  
 *$startingLoc*  
 Punto della stringa di origine corrispondente al punto iniziale della sottostringa. Se il valore è negativo o è uguale a 0, vengono restituiti solo i caratteri nelle posizioni maggiori di zero. Se è maggiore della lunghezza del *$sourceString*, viene restituita la stringa di lunghezza zero.  
  
 *$length*  
 Numero di caratteri da recuperare (facoltativo). Se non specificato, restituisce tutti i caratteri dalla posizione specificata *$startingLoc* fino alla fine della stringa.  
  
## <a name="remarks"></a>Note  
 La versione della funzione con tre argomenti restituisce i caratteri di `$sourceString` il cui operatore di posizione `$p` è soggetto alla regola seguente:  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 Il valore di *$length* può essere maggiore del numero di caratteri nel valore di *$sourceString* successivi alla posizione iniziale. In questo caso, la sottostringa restituisce i caratteri fino alla fine della *$sourceString*.  
  
 Il primo carattere di una stringa si trova nella posizione 1.  
  
 Se il valore di *$sourceString* è una sequenza vuota, viene gestita come stringa di lunghezza zero. In caso contrario, se uno dei due *$startingLoc* oppure *$length* è una sequenza vuota, viene restituita la sequenza vuota.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caratteri supplementari (coppie di surrogati)  
 Il comportamento delle coppie di surrogati nelle funzioni XQuery dipende dal livello di compatibilità del database e, in alcuni casi, dall'URI dello spazio dei nomi predefinito per le funzioni. Per altre informazioni, vedere la sezione "XQuery funzioni riconoscono i surrogati" nell'argomento [le modifiche di rilievo alle funzionalità del motore di Database in SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Vedere anche [livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) e [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="implementation-limitations"></a>Limitazioni di implementazione  
 SQL Server richiede la *$startingLoc* e *$length parametri* sia di tipo xs: decimal anziché di xs: Double.  
  
 SQL Server consente *$startingLoc* e *$length* rappresentino la sequenza vuota, perché la sequenza vuota è un possibile valore risultante di errori dinamici viene eseguito il mapping a ().  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo i [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] database.  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>R. Utilizzo della funzione XQuery substring() per recuperare le descrizioni parziali del modello del prodotto disponibili nell'elemento Summary  
 La query recupera i primi 50 caratteri del testo che descrive il modello di prodotto, la <`Summary`> elemento del documento.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Il **String ()** funzione restituisce il valore della stringa di <`Summary`> elemento. Questa funzione viene utilizzata, in quanto il <`Summary`> elemento contiene sia il testo e formattazione html (elementi), i sottoelementi e perché si ignorerà questi elementi e recuperare tutto il testo.  
  
-   Il **substring** funzione recupera i primi 50 caratteri del valore stringa recuperato dalle **String ()** .  
  
 Risultato parziale:  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
