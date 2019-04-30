---
title: Funzione Min (XQuery) | Microsoft Docs
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
- fn:min function
- min function [XQuery]
ms.assetid: db0b7d94-3fa6-488f-96d6-6a9a7d6eda23
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 69381eb0ffdd3638079d824d8d4c150563375a6c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046965"
---
# <a name="aggregate-functions---min"></a>Funzioni di aggregazione - min
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Da una sequenza di valori atomici, restituisce *$arg*, l'unico elemento il cui valore è minore di quello di tutti gli altri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:min($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Sequenza di elementi da cui viene restituito il valore minimo.  
  
## <a name="remarks"></a>Note  
 Tutti i tipi di valori atomizzati passati a **min ()** devono essere sottotipi dello stesso tipo di base. Tipi di base accettati sono i tipi che supportano il **gt** operazione. Tra questi tipi sono inclusi i tre tipi di base numerici predefiniti, ovvero i tipi di base di data/ora xs:string, xs:boolean e xdt:untypedAtomic. Per i valori di tipo xdt:untypedAtomic viene eseguito il cast a xs:double. Se c'è una combinazione di questi tipi, o se vengono passati altri valori di altri tipi, viene generato un errore statico.  
  
 Il risultato del **min ()** riceve il tipo di base dei tipi passati, ad esempio xs: double nel caso di xdt: untypedAtomic. Se l'input è una sequenza vuota calcolata in modo statico, la sequenza vuota è implicita e viene restituito un errore statico.  
  
 Il **min ()** funzione restituisce un valore nella sequenza di dimensioni inferiori a quelle di qualsiasi altro nella sequenza di input. Per i valori xs:string, vengono utilizzate le regole di confronto predefinite dei punti di codice Unicode. Se non è possibile eseguire il cast di un valore xdt: untypedAtomic a xs: Double, il valore viene ignorato nella sequenza di input *$arg*. Se l'input è una sequenza vuota calcolata in modo dinamico, viene restituita la sequenza vuota.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo nel database AdventureWorks.  
  
### <a name="a-using-the-min-xquery-function-to-find-the-work-center-location-that-has-the-fewest-labor-hours"></a>A. Utilizzo della funzione XQuery min() per l'individuazione del centro di lavorazione con il numero minimo di ore di manodopera  
 La query seguente recupera tutti i centri di lavorazione con il numero minimo di ore di manodopera inclusi nel processo di produzione del modello del prodotto (ProductModelID=7). In genere, come illustrato nell'esempio seguente, viene restituito un singolo centro. Nel caso in cui esistano più centri con lo stesso numero minimo di ore di manodopera, vengono restituiti tutti questi centri.  
  
```  
select ProductModelID, Name, Instructions.query('  
  declare namespace AWMI=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  for   $Location in /AWMI:root/AWMI:Location  
  where $Location/@LaborHours =  
          min( /AWMI:root/AWMI:Location/@LaborHours )  
return  
  <Location WCID=     "{ $Location/@LocationID }"   
              LaborHrs= "{ $Location/@LaborHours }" />  
  ') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Il **dello spazio dei nomi** parola chiave nel prologo della XQuery definisce un prefisso dello spazio dei nomi. In seguito, tale prefisso viene utilizzato nel corpo della query XQuery.  
  
 Corpo della query XQuery costruisce il codice XML con un \<percorso > elemento con WCID e **LaborHrs** attributi.  
  
-   La query recupera inoltre i valori del modello del prodotto ProductModelID e dei nomi.  
  
 Questo è il risultato:  
  
```  
ProductModelID   Name              Result  
---------------  ----------------  ---------------------------------  
7                HL Touring Frame  <Location WCID="45" LaborHrs="0.5"/>   
```  
  
## <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Il **min ()** funzione esegue il mapping di tutti i valori interi a xs: decimal.  
  
-   Il **min ()** funzione con valori di tipo xs: Duration non è supportata.  
  
-   Non sono supportate le sequenze con combinazioni di tipi che non rispettano i limiti del tipo di base.  
  
-   Non è supportata l'opzione sintattica che fornisce le regole di confronto.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
