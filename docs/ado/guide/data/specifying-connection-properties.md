---
description: Specifica delle proprietà di connessione
title: Impostazione delle proprietà di connessione | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 0c4d3a70388415402db3ecf8bdb21bd717a66aa6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979562"
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
