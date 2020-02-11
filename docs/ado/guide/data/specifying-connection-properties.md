---
title: Impostazione delle proprietà di connessione | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5aee5946f3087956a0117b88f4044ef8a6c9bd9f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924134"
---
# <a name="specifying-connection-properties"></a>Specifica delle proprietà di connessione
È possibile specificare la maggior parte delle informazioni specificate da una [stringa di connessione](../../../ado/guide/data/creating-a-connection-string.md) impostando le proprietà dell'oggetto **connessione** prima di aprire la connessione. Ad esempio, è possibile ottenere lo stesso effetto della stringa di connessione descritta in [creazione di una stringa di connessione](../../../ado/guide/data/creating-a-connection-string.md) usando il codice seguente.  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 DefaultDatabase viene impostato solo dopo l'apertura della connessione.  
  
> [!NOTE]
>  In ADO non è necessario usare una password contenente punti e virgola (";"), a meno che la password non sia racchiusa tra virgolette singole.
