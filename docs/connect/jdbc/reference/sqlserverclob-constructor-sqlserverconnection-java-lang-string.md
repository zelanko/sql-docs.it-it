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
manager: jroth
ms.openlocfilehash: a454567f031d935b6bfcdd8d5d32a6d2bead380f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803138"
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
  
  
