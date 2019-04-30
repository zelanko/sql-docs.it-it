---
title: Funzione Count (XQuery) | Microsoft Docs
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
- fn:count function
- count function [XQuery]
ms.assetid: a9f7131f-23e1-4d4d-a36c-180447543926
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 30ec1817d4f22ff8ee23746f925943397981382f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046922"
---
# <a name="aggregate-functions---count"></a>Funzioni di aggregazione - count
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce il numero di elementi contenuti nella sequenza specificata da *$arg*.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:count($arg as item()*) as xs:integer  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Elementi da contare.  
  
## <a name="remarks"></a>Note  
 Restituisce 0 se *$arg* è una sequenza vuota.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo nel database AdventureWorks.  
  
### <a name="a-using-the-count-xquery-function-to-count-the-number-of-work-center-locations-in-the-manufacturing-of-a-product-model"></a>A. Utilizzo della funzione XQuery count() per il conteggio del numero di centri di lavorazione nella produzione di un modello di prodotto  
 La query seguente conta il numero di centri di lavorazione nel processo di produzione di un modello di prodotto (ProductModelID=7).  
  
```  
SELECT Production.ProductModel.ProductModelID,   
       Production.ProductModel.Name,   
       Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations>  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID=7  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Il **dello spazio dei nomi** parola chiave nella [prologo XQuery](../xquery/modules-and-prologs-xquery-prolog.md) definisce un prefisso dello spazio dei nomi. Il prefisso viene quindi utilizzato nel corpo della query XQuery.  
  
-   La query costruisce codice XML che include il <`NoOfWorkStations`> elemento.  
  
-   Il **Count ()** funzionare nei conteggi di corpo della query XQuery il numero di <`Location`> elementi.  
  
 Questo è il risultato:  
  
```  
ProductModelID   Name                 WorkCtrCount       
-------------- ---------------------------------------------------  
7             HL Touring Frame  <NoOfWorkStations>6</NoOfWorkStations>     
```  
  
 È inoltre possibile costruire il codice XML in modo che includa ID e nome del modello di prodotto, come illustrato nella query seguente:  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations  
             ProductModelID= "{ sql:column("Production.ProductModel.ProductModelID") }"   
             ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID= 7  
```  
  
 Questo è il risultato:  
  
```  
<NoOfWorkStations ProductModelID="7"   
                  ProductModelName="HL Touring Frame">6</NoOfWorkStations>  
```  
  
 È possibile ottenere la restituzione dei valori in un tipo non xml, come illustrato nella query seguente. La query Usa la [metodo Value () (tipo di dati xml)](../t-sql/xml/value-method-xml-data-type.md) per recuperare il numero di località di lavoro center.  
  
```  
SELECT  ProductModelID,   
        Name,   
        Instructions.value('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
           count(/AWMI:root/AWMI:Location)', 'int' ) as WorkCtrCount  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Questo è il risultato:  
  
```  
ProductModelID    Name            WorkCtrCount  
-------------- ---------------------------------  
7              HL Touring Frame        6     
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
