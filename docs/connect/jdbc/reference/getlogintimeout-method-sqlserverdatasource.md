---
title: Metodo getLoginTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5fe82d2709aa8efa32408a9d9d86f0f660bed823
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67982552"
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>Metodo getLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il numero di secondi di attesa di questo oggetto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) durante il tentativo di stabilire una connessione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che rappresenta il numero di secondi di attesa.  
  
## <a name="remarks"></a>Osservazioni  
 Se l'applicazione non specifica in modo esplicito un valore di timeout, questo metodo restituisce un valore predefinito di 15 secondi.  
  
 Questo metodo getLoginTimeout viene specificato dal metodo getLoginTimeout nell'interfaccia javax.sql.DataSource.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
