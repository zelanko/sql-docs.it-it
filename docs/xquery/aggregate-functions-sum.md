---
title: Funzione SUM (XQuery) | Microsoft Docs
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
- sum function [XQuery]
- fn:sum function
ms.assetid: 12288f37-b54c-4237-b75e-eedc5fe8f96d
author: rothja
ms.author: jroth
ms.openlocfilehash: 9e9095fdecf9bdf9782815c8b44c2131313568c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985749"
---
# <a name="aggregate-functions---sum"></a>Funzioni di aggregazione - sum
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce la somma di una sequenza di numeri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:sum($arg as xdt:anyAtomicType*) as xdt:anyAtomicType  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Sequenza di valori atomici per i quali deve essere calcolata la somma.  
  
## <a name="remarks"></a>Note  
 Tutti i tipi di valori atomizzati passati a **SUM ()** devono essere sottotipi dello stesso tipo di base. I tipi di base accettati sono i tre tipi numerici di base predefiniti o xdt:untypedAtomic. Per i valori di tipo xdt:untypedAtomic viene eseguito il cast a xs:double. Se c'è una combinazione di questi tipi, o se vengono passati altri valori di altri tipi, viene generato un errore statico.  
  
 Il risultato del **SUM ()** riceve il tipo di base dei tipi passati, ad esempio xs: double nel caso di xdt: untypedAtomic, anche se l'input è facoltativamente la sequenza vuota. Se l'input è costituito da dati statici vuoti, il risultato sarà 0 con il tipo statico e dinamico di xs:integer.  
  
 Il **SUM ()** funzione restituisce la somma dei valori numerici. Se non è possibile eseguire il cast di un valore xdt: untypedAtomic a xs: Double, il valore viene ignorato nella sequenza di input *$arg*. Se l'input è una sequenza vuota calcolata in modo dinamico, viene restituito il valore 0 del tipo di base utilizzato.  
  
 Se si verifica un overflow o un'eccezione di valori non compresi nell'intervallo, la funzione restituisce un errore di run-time.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo i [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] database.  
  
### <a name="a-using-the-sum-xquery-function-to-find-the-total-combined-number-of-labor-hours-for-all-work-center-locations-in-the-manufacturing-process"></a>R. Utilizzo della funzione XQuery sum() per trovare il numero totale combinato delle ore di manodopera relativo a tutti i centri di lavorazione del processo di produzione  
 La query seguente trova il numero totale delle ore di manodopera relativo a tutti i centri di lavorazione del processo di produzione per tutti i modelli di prodotto per i quali sono state archiviate istruzioni di produzione.  
  
```  
SELECT Instructions.query('         
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
  <ProductModel PMID= "{ sql:column("Production.ProductModel.ProductModelID") }"         
  ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >         
   <TotalLaborHrs>         
     { sum(//AWMI:Location/@LaborHours) }         
   </TotalLaborHrs>         
 </ProductModel>         
    ') as Result         
FROM Production.ProductModel         
WHERE Instructions is not NULL         
```  
  
 Di seguito è riportato il risultato parziale.  
  
```  
<ProductModel PMID="7" ProductModelName="HL Touring Frame">  
   <TotalLaborHrs>12.75</TotalLaborHrs>  
</ProductModel>  
<ProductModel PMID="10" ProductModelName="LL Touring Frame">  
  <TotalLaborHrs>13</TotalLaborHrs>  
</ProductModel>  
...  
```  
  
 Anziché restituire il risultato come codice XML, è possibile scrivere la query in modo da generare risultati relazionali, come illustrato nella query seguente:  
  
```  
SELECT ProductModelID,         
        Name,         
        Instructions.value('declare namespace   
      AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
    sum(//AWMI:Location/@LaborHours)', 'float') as TotalLaborHours         
FROM Production.ProductModel         
WHERE Instructions is not NULL          
```  
  
 Risultato parziale:  
  
```  
ProductModelID Name                 TotalLaborHours         
-------------- -------------------------------------------------  
7              HL Touring Frame           12.75                   
10             LL Touring Frame           13                      
43             Touring Rear Wheel         3                       
...  
```  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Solo la versione singolo argomento del **SUM ()** è supportata.  
  
-   Se l'input è una sequenza vuota calcolata in modo dinamico, viene restituito il valore 0 del tipo di base utilizzato anziché il tipo xs:integer.  
  
-   Il **SUM ()** funzione esegue il mapping di tutti i valori interi a xs: decimal.  
  
-   Il **SUM ()** funzione con valori di tipo xs: Duration non è supportata.  
  
-   Non sono supportate le sequenze con combinazioni di tipi che non rispettano i limiti del tipo di base.  
  
-   Se, xs genera un errore di dominio.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
