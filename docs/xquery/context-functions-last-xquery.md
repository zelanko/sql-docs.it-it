---
title: Funzione Last (XQuery) | Microsoft Docs
description: Informazioni sulla funzione XQuery last () che restituisce l'indice Integer dell'ultimo elemento in una sequenza.
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
- last function [XQuery]
- fn:last function
ms.assetid: dc92086e-3b01-4b0b-9f54-3bbf306cf7ae
author: rothja
ms.author: jroth
ms.openlocfilehash: f88c438206551e170810f467e7944b21232e245d
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529705"
---
# <a name="context-functions---last-xquery"></a>Funzioni di contesto - last (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce il numero di elementi della sequenza da elaborare. In particolare, restituisce l'indice di valori interi dell'ultimo elemento della sequenza. Il valore di indice del primo elemento della sequenza è 1.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:last() as xs:integer  
```  
  
## <a name="remarks"></a>Osservazioni  
 In SQL Server, **FN: Last ()** può essere usato solo nel contesto di un predicato dipendente dal contesto. In particolare, può essere utilizzata solo tra parentesi (`[ ]`).  
  
## <a name="examples"></a>Esempio  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse colonne di tipo **XML** nel database AdventureWorks.  
  
### <a name="a-using-the-last-xquery-function-to-retrieve-the-last-two-manufacturing-steps"></a>A. Utilizzo della funzione XQuery last() per recuperare le ultime due fasi di produzione  
 La query seguente recupera le ultime due fasi di produzione relative a un modello di prodotto specifico. Il valore, il numero di fasi di produzione, restituito dalla funzione **Last ()** viene utilizzato in questa query per recuperare le ultime due fasi di produzione.  
  
```  
SELECT ProductModelID, Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Nella query precedente, la funzione **Last ()** in/ `/AWMI:root//AWMI:Location)[1]/AWMI:step[last()]` restituisce il numero di fasi di produzione. Tale valore viene utilizzato per recuperare l'ultima fase di produzione nel centro di lavorazione.  
  
 Risultato:  
  
```  
ProductModelID Result    
-------------- -------------------------------------  
7      <LastTwoManuSteps>  
         <Last-1Step>  
            When finished, inspect the forms for defects per   
            Inspection Specification .  
         </Last-1Step>  
         <LastStep>Remove the frames from the tool and place them   
            in the Completed or Rejected bin as appropriate.  
         </LastStep>  
       </LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
