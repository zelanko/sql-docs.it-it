---
title: "Esempio: ridenominazione dell'elemento &lt;row&gt; | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3780bb0f35c65003f7a5bdb126ca7597786758a9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716910"
---
# <a name="example-renaming-the-ltrowgt-element"></a>Esempio: ridenominazione dell'elemento &lt;row&gt;
  Nella modalità RAW viene creato un elemento `<row>`per ogni riga del set di risultati. È possibile specificare un nome diverso per l'elemento impostando un argomento facoltativo per la modalità RAW, come illustrato nella query seguente. La query restituisce un elemento <`ProductModel`> per ogni riga del set di righe.  
  
## <a name="example"></a>Esempio  
  
```  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122  
FOR XML RAW ('ProductModel'), ELEMENTS  
GO  
```  
  
 Di seguito è riportato il risultato. Nella query viene aggiunta la direttiva `ELEMENTS` e pertanto il risultato è incentrato sugli elementi.  
  
```  
<ProductModel>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</ProductModel>   
```  
  
## <a name="see-also"></a>Vedere anche  
 [Usare la modalità RAW con FOR XML](use-raw-mode-with-for-xml.md)  
  
  
