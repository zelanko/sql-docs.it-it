---
title: Specificare XSINIL con la direttiva ELEMENTS | Microsoft Docs
description: Visualizzare un esempio in cui XSINIL viene specificato con la direttiva ELEMENTS per generare codice XML incentrato sugli elementi dai risultati della query.
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, specifying XSINIL example
ms.assetid: 07c873ff-1f9d-480e-8536-862c39eb8249
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: ce76de4ec22727a99e2dbd7ad707fc3a861c315e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632310"
---
# <a name="example-specifying-xsinil-with-the-elements-directive"></a>Esempio: specifica di XSINIL con la direttiva ELEMENTS
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
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
 [Usare la modalità RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
