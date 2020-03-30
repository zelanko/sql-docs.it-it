---
title: Costruttore SQLServerClob (SQLServerConnection, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.SQLServerClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7058f4f7-ef3e-4d62-90d1-79299708b1eb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7a539ef893788be9e0200b9f412f8c3ed7652b26
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67971806"
---
# <a name="sqlserverclob-constructor-sqlserverconnection-javalangstring"></a>Costruttore SQLServerClob (SQLServerConnection, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inizializza una nuova istanza della classe [SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md) se sono specificati un oggetto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) e una stringa di dati.  
  
> [!NOTE]  
>  Questo metodo è deprecato nella versione 2.0 del driver JDBC. Usare invece il metodo [createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md) della classe [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public SQLServerClob(SQLServerConnection connection,  
                     java.lang.String data)  
```  
  
#### <a name="parameters"></a>Parametri  
 *connection*  
  
 Oggetto SQLServerConnection.  
  
 *data*  
  
 I dati CLOB.  
  
## <a name="see-also"></a>Vedere anche  
 [Costruttori di SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-constructors.md)   
 [Membri di SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
