---
title: 'Esempio: specifica di un elemento radice per codice XML generato da FOR XML | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, specifying root element example
- RAW mode, with FOR XML example
ms.assetid: bcc54b11-0713-4e43-8dbe-d6f3ad1993b5
author: rothja
ms.author: jroth
ms.openlocfilehash: ab9253727389e29973ee1f4b5ce38ce94ca86670
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067853"
---
# <a name="example-specifying-a-root-element-for-the-xml-generated-by-for-xml"></a>Esempio: specifica di un elemento radice per codice XML generato da FOR XML
  Specificando l'opzione `ROOT` nella query `FOR XML` , è possibile richiedere un singolo elemento di livello principale per il codice XML risultante, come illustrato nella query seguente. L'argomento specificato per la direttiva `ROOT` consente di ottenere il nome dell'elemento radice.  
  
## <a name="example"></a>Esempio  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119 or ProductModelID=115  
FOR XML RAW, ROOT('MyRoot')  
go  
```  
  
 Risultato:  
  
```  
<MyRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
  <row ProductModelID="115" Name="Cable Lock" />  
</MyRoot>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Usare la modalità RAW con FOR XML](use-raw-mode-with-for-xml.md)  
  
  
