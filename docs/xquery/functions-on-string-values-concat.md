---
title: Funzione Concat (XQuery) | Microsoft Docs
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
- fn:concat function
- concat function [XQuery]
ms.assetid: d50afd20-a297-445e-be9e-13b48017e7ca
author: rothja
ms.author: jroth
ms.openlocfilehash: 063eca49a6a4d69e84e8a3d05221b632d0690bef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099833"
---
# <a name="functions-on-string-values---concat"></a>Funzioni su valori stringa - concat
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Accetta zero o più stringhe come argomenti e restituisce una stringa creata concatenando i valori di ognuno di questi argomenti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:concat ($string as xs:string?  
           ,$string as xs:string?  
           [, ...]) as xs:string  
```  
  
## <a name="arguments"></a>Argomenti  
 *$string*  
 Stringa facoltativa per la concatenazione.  
  
## <a name="remarks"></a>Note  
 La funzione richiede almeno due argomenti. Se un argomento è costituito da una sequenza vuota, viene considerato come stringa di lunghezza zero.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caratteri supplementari (coppie di surrogati)  
 Il comportamento delle coppie di surrogati nelle funzioni XQuery dipende dal livello di compatibilità del database e, in alcuni casi, dall'URI dello spazio dei nomi predefinito per le funzioni. Per altre informazioni, vedere la sezione "XQuery funzioni riconoscono i surrogati" nell'argomento [le modifiche di rilievo alle funzionalità del motore di Database in SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Vedere anche [livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) e [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo nel database di esempio AdventureWorks.  
  
### <a name="a-using-the-concat-xquery-function-to-concatenate-strings"></a>R. Utilizzo della funzione XQuery concat() per la concatenazione di stringhe  
 Per un modello di prodotto specifico, questa query restituisce una stringa creata concatenando il periodo di validità e la descrizione della garanzia. Nel documento di descrizione del catalogo, la <`Warranty`> elemento è costituito da <`WarrantyPeriod`> e <`Description`> gli elementi figlio.  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"  
        ProductModelName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE  PD.ProductModelID=28  
  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Nella clausola SELECT, CatalogDescription è una **xml** colonna di tipo. Pertanto, il [metodo query () (tipo di dati XML)](../t-sql/xml/query-method-xml-data-type.md), ovvero Instructions, viene usato. L'istruzione XQuery viene specificata come argomento per il metodo di query.  
  
-   Nel documento sul quale viene eseguita la query vengono utilizzati spazi dei nomi. Pertanto, il **dello spazio dei nomi** parola chiave viene usata per definire il prefisso dello spazio dei nomi. Per altre informazioni, vedere [prologo XQuery](../xquery/modules-and-prologs-xquery-prolog.md).  
  
 Questo è il risultato:  
  
```  
<Product ProductModelID="28" ProductModelName="Road-450">1 year-parts and labor</Product>  
```  
  
 La query precedente recupera le informazioni relative a un prodotto specifico. La query seguente recupera le stesse informazioni per tutti i prodotti per i quali vengono archiviate descrizioni di catalogo XML. Il **exist ()** metodo per il **xml** tipo di dati nella clausola WHERE restituisce True se il documento XML nelle righe ha una <`ProductDescription`> elemento.  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"   
        ProductName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE CatalogDescription.exist('//pd:ProductDescription ') = 1  
  
```  
  
 Si noti che il valore booleano restituito dal **exist ()** metodo per il **xml** tipo viene confrontato con 1.  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Il **Concat ()** funzione in SQL Server accetta solo valori di tipo xs: String. Per gli altri valori è necessario eseguire il cast esplicito al tipo xs:string o al tipo xdt:untypedAtomic.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
