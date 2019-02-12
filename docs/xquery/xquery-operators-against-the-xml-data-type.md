---
title: Operatori di XQuery per il tipo di dati xml | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, operators
- operators [XQuery]
- xml data type [SQL Server], XQuery
ms.assetid: 39ca3d2e-e928-4333-872b-75c4ccde8e79
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2786295b344cfc2df6ae613e42a39f71aee4d3d8
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56038892"
---
# <a name="xquery-operators-against-the-xml-data-type"></a>Operatori di XQuery per il tipo di dati xml
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery supporta gli operatori seguenti:  
  
-   Operatori numerici (+, -, *, div, mod)  
  
-   Operatori di confronto per i valori (eq, ne, lt, gt, le, ge)  
  
-   Operatori di confronto generali (=,! =, \<, >, \<=, > =)  
  
 Per altre informazioni su questi operatori, vedere [espressioni di confronto &#40;XQuery&#41;](../xquery/comparison-expressions-xquery.md)  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-general-operators"></a>A. Utilizzo degli operatori generali  
 La query seguente illustra l'utilizzo degli operatori generali validi per le sequenze e inoltre per le sequenze di confronto. La query recupera una sequenza di numeri di telefono per ogni cliente dal **AdditionalContactInfo** della colonna della **contatto** tabella. La sequenza viene quindi confrontata con la sequenza di due numeri di telefono ("111-111-1111", "222-2222").  
  
 La query Usa la **=** operatore di confronto. Ogni nodo nella sequenza sul lato destro del **=** operatore viene confrontato con ogni nodo nella sequenza di sinistra. Se i nodi corrispondono, il confronto nodo viene **TRUE**. Viene quindi convertito in un tipo di dati int e confrontato con 1, quindi la query restituisce l'ID del cliente.  
  
```sql
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS ACI,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.value('  
      //ACI:AdditionalContactInfo//ACT:telephoneNumber/ACT:number =   
          ("111-111-1111", "222-2222")',  
      'bit')= cast(1 as bit)  
```  
  
 È presente un altro modo per osservare come funziona la query precedente: Ogni valore di numero telefonico telefono recuperati dal **AdditionalContactInfo** colonna viene confrontata con il set di due numeri di telefono. Se il numero è presente nel set, nel risultato viene restituito il cliente.  
  
### <a name="b-using-a-numeric-operator"></a>b. Utilizzo di un operatore numerico  
 L'operatore + nella query è un operatore per i valori, perché viene applicato a un singolo elemento. Ad esempio, il valore 1 viene aggiunto alle dimensioni di un lotto restituite dalla query:  
  
```sql
SELECT ProductModelID, Instructions.query('  
     declare namespace   
 AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in (/AWMI:root/AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"  
                   LotSize  = "{  number($i/@LotSize) }"  
                   LotSize2 = "{ number($i/@LotSize) + 1 }"  
                   LotSize3 = "{ number($i/@LotSize) + 2 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
### <a name="c-using-a-value-operator"></a>C. Utilizzo di un operatore per valori  
 La query seguente recupera gli elementi <`Picture`> per un modello di prodotto per cui le dimensioni dell'immagine sono "small":  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]  
     return  
           $P  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Poiché entrambi gli operandi per il **eq** operatore sono valori atomici, l'operatore di valore viene usato nella query. È possibile scrivere la stessa query usando l'operatore di confronto generali ( **=** ).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati xml](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [Dati XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Riferimento al linguaggio XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
