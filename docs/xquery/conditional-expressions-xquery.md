---
title: Espressioni condizionali (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, conditional expressions
- expressions [XQuery], conditional
- effective Boolean value [XQuery]
- if-then-else statement [XQuery]
- conditional expressions [XQuery]
- EBV
ms.assetid: b280dd96-c80f-4c51-bc06-a88d42174acb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 62a061632b5f598932fe29499519d7eb897c78a6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041742"
---
# <a name="conditional-expressions-xquery"></a>Espressioni condizionali (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery supporta il seguente parametro condizionale **if-then-else** istruzione:  
  
```  
if (<expression1>)  
then  
  <expression2>  
else  
  <expression3>  
```  
  
 In base al valore booleano effettivo di `expression1`, viene valutata `expression2` oppure `expression3`. Ad esempio:  
  
-   Se l'espressione di test `expression1` restituisce una sequenza vuota, il risultato è False.  
  
-   Se l'espressione di test `expression1` restituisce un valore booleano semplice, tale valore è il risultato dell'espressione.  
  
-   Se l'espressione di test `expression1` restituisce una sequenza di uno o più nodi, il risultato dell'espressione è True.  
  
-   Negli altri casi, viene restituito un errore statico.  
  
 Si noti inoltre quanto segue:  
  
-   L'espressione di test deve essere racchiusa tra parentesi.  
  
-   Il **else** è necessaria l'espressione. Se non è necessaria, è possibile restituire " ( ) ", come illustrato negli esempi disponibili in questa sezione.  
  
 Ad esempio, la query seguente viene specificata con il **xml** variabile di tipo. Il **se** condizione testa il valore della variabile SQL (@v) all'interno dell'espressione XQuery utilizzando la [funzione SQL: variable](../xquery/xquery-extension-functions-sql-variable.md) funzione dell'estensione. Se il valore della variabile è "FirstName", restituisce l'elemento <`FirstName`>. In caso contrario, restituisce l'elemento <`LastName`>.  
  
```  
declare @x xml  
declare @v varchar(20)  
set @v='FirstName'  
set @x='  
<ROOT rootID="2">  
  <FirstName>fname</FirstName>  
  <LastName>lname</LastName>  
</ROOT>'  
SELECT @x.query('  
if ( sql:variable("@v")="FirstName" ) then  
  /ROOT/FirstName  
 else  
   /ROOT/LastName  
')  
```  
  
 Questo è il risultato:  
  
```  
<FirstName>fname</FirstName>  
```  
  
 La query seguente recupera le prime due descrizioni di caratteristiche dalla descrizione di catalogo di uno specifico modello di prodotto. Se il documento contiene altre caratteristiche, aggiunge un elemento <`there-is-more`> con contenuto vuoto.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /p1:ProductDescription/@ProductModelID }  
          { /p1:ProductDescription/@ProductModelName }   
          {  
            for $f in /p1:ProductDescription/p1:Features/*[position()\<=2]  
            return  
            $f   
          }  
          {  
            if (count(/p1:ProductDescription/p1:Features/*) > 2)  
            then \<there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Nella query precedente, la condizione nel **se** espressione controlla se sono presenti più di due elementi figlio <`Features`>. In caso affermativo, restituisce l'elemento `\<there-is-more/>` nel risultato.  
  
 Questo è il risultato:  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  \<p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p1:WarrantyPeriod>3 years\</p1:WarrantyPeriod>  
    \<p1:Description>parts and labor\</p1:Description>  
  \</p1:Warranty>  
  \<p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    \<p2:NoOfYears>10 years\</p2:NoOfYears>  
    \<p2:Description>maintenance contract available through your dealer or any AdventureWorks retail store.\</p2:Description>  
  \</p2:Maintenance>  
  \<there-is-more />  
</Product>  
```  
  
 Nella query seguente viene restituito un elemento con un attributo <`Location`> se il centro di lavorazione non specifica le ore di preparazione (SetupHours).  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in //AWMI:root/AWMI:Location  
        return  
        if ( $WC[not(@SetupHours)] )  
        then  
          <WorkCenterLocation>  
             { $WC/@LocationID }   
          </WorkCenterLocation>  
         else  
           ()  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Questo è il risultato:  
  
```  
<WorkCenterLocation LocationID="30" />  
<WorkCenterLocation LocationID="45" />  
<WorkCenterLocation LocationID="60" />  
```  
  
 Questa query può essere scritta senza i **se** clausola, come illustrato nell'esempio seguente:  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in //AWMI:root/AWMI:Location[not(@SetupHours)]   
        return  
          <Location>  
             { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni XQuery](../xquery/xquery-expressions.md)  
  
  
