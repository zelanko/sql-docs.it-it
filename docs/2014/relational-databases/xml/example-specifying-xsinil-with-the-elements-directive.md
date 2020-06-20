---
title: 'Esempio: specifica di XSINIL con la direttiva ELEMENTS | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, specifying XSINIL example
ms.assetid: 07c873ff-1f9d-480e-8536-862c39eb8249
author: rothja
ms.author: jroth
ms.openlocfilehash: 4e736beb22f40008d2a8aa5fac797b9f48904c52
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85013295"
---
# <a name="example-specifying-xsinil-with-the-elements-directive"></a>Esempio: specifica di XSINIL con la direttiva ELEMENTS
  Nella query seguente viene specificata la direttiva `ELEMENTS` per generare codice XML incentrato sugli elementi dai risultati della query.  
  
## <a name="example"></a>Esempio  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS;  
GO  
```  
  
 Di seguito è riportato il risultato parziale.  
  
```  
<row>  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
 Nella colonna `Color` sono presenti i valori Null per alcuni prodotti e pertanto nel codice XML risultante non verrà generato l'elemento <`Color`> corrispondente. Se si aggiunge la direttiva `XSINIL` insieme a `ELEMENTS`, è possibile generare l'elemento <`Color`> anche per i valori Null relativi al colore nel set dei risultati.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS XSINIL ;  
```  
  
 Risultato parziale:  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
  <Color xsi:nil="true" />  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Usare la modalità RAW con FOR XML](use-raw-mode-with-for-xml.md)  
  
  
