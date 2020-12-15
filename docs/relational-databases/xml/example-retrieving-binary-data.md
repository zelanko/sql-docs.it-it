---
title: 'Esempio: Recupero di dati binari | Microsoft Docs'
description: Visualizzare un esempio di query SQL che recupera dati binari usando le opzioni RAW e BINARY BASE64 con la clausola FOR XML.
ms.custom: ''
ms.date: 04/03/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
author: RothJa
ms.author: jroth
ms.openlocfilehash: fedec9e351b9c8910db0bee51c1e2c5dc8569655
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97402981"
---
# <a name="example-retrieving-binary-data"></a>Esempio: Recupero di dati binari

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

La query seguente restituisce la foto del prodotto archiviata in una colonna di tipo **varbinary(max)** . L'opzione `BINARY BASE64` specificata nella query consente di restituire i dati binari nel formato con codifica Base64.

## <a name="example"></a>Esempio

```sql
USE AdventureWorks2012;
GO
SELECT ProductPhotoID, ThumbNailPhoto
FROM Production.ProductPhoto
WHERE ProductPhotoID=1
FOR XML RAW, BINARY BASE64 ;
GO
```

Il risultato previsto è il seguente:

```console
<row ProductModelID="1" ThumbNailPhoto="base64 encoded binary data"/>
```

## <a name="see-also"></a>Vedere anche

[Usare la modalità RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)
