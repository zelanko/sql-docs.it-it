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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6fee9745bca206f00603b32a6c4cd29faab34eca
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760837"
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
