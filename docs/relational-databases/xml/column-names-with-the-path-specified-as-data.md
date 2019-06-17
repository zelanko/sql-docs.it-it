---
title: Nomi di colonna con il percorso specificato come data() | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: 0b738e44-6108-4417-a9a4-abeb7680d899
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77913ea6358f9a5d1b88de7426144b730b5c74e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66175365"
---
# <a name="column-names-with-the-path-specified-as-data"></a>Nomi di colonna con il percorso specificato come dati()

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Se il percorso specificato come nome di colonna è "data()", il valore viene gestito nel codice XML generato come valore atomico. Se anche l'elemento successivo nella serializzazione è un valore atomico, al codice XML viene aggiunto uno spazio. Ciò risulta utile quando si creano valori di elementi e di attributi di tipo elenco. La query seguente recupera l'ID del modello di prodotto e l'elenco dei prodotti di quel modello.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ProductModelID       AS "@ProductModelID",  
       Name                 AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
      FOR XML PATH (''))    AS "@ProductIDs"  
FROM  Production.ProductModel  
WHERE ProductModelID= 7   
FOR XML PATH('ProductModelData');  
```  
  
 L'istruzione SELECT nidificata recupera un elenco di ID di prodotti e specifica "data()" come nome di colonna per gli ID di prodotto. Poiché la modalità PATH specifica una stringa vuota per il nome dell'elemento riga, non viene generato alcun elemento riga. I valori vengono invece restituiti come assegnati a un attributo ProductIDs dell'elemento riga `<ProductModelData>` dell'istruzione SELECT padre. Risultato:  

```sql
<ProductModelData
  ProductModelID="7"
  ProductModelName="HL Touring Frame"
  ProductIDs="885 887 888 889 890 891 892 893"
/>
```

## <a name="see-also"></a>Vedere anche  
 [Utilizzare la modalità PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
