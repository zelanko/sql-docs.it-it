---
title: Metodo getLockTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 676094e9-ec18-4524-9b21-1f9c5b16dd52
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9c94e0c69bd528f1c579f41319a4db18b7d4d3c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67982567"
---
# <a name="getlocktimeout-method-sqlserverdatasource"></a>Metodo getLockTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un valore **int** che indica il numero di millisecondi di attesa prima che il database segnali un timeout di blocco.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getLockTimeout()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** contenente il numero di millisecondi di attesa del database.  
  
## <a name="remarks"></a>Osservazioni  
 Il timeout di blocco è il numero di millisecondi di attesa prima che venga segnalato un timeout di blocco per il database. Il valore predefinito -1 indica un'attesa illimitata. Se specificato, questo valore diventerà l'impostazione predefinita per tutte le istruzioni sulla connessione.  
  
> [!NOTE]  
>  Un valore pari a 0 indica che non vi sarà attesa. Se la proprietà lockTimeout non è impostata, il metodo getLockTimeout restituisce il valore predefinito -1.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
