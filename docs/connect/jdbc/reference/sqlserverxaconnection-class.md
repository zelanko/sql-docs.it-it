---
title: Classe SQLServerXAConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 177b10c9657c4cb8d6b37f7dec9d3b860308dcb7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788901"
---
# <a name="sqlserverxaconnection-class"></a>Classe SQLServerXAConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Rappresenta le connessioni JDBC che possono partecipare alle transazioni distribuite (XA).  
  
 **Pacchetto:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **Implementa:** javax.sql.XAConnection  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>Remarks  
 Un oggetto SQLServerXAConnection può essere integrato in una transazione distribuita tramite un oggetto [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md). Un responsabile transazioni, generalmente parte di un server di livello intermedio, gestisce un oggetto SQLServerXAConnection tramite l'oggetto SQLServerXAResource.  
  
> [!NOTE]  
>  I programmatori di applicazioni in genere non utilizzano direttamente questa interfaccia. Viene utilizzata principalmente da un responsabile transazioni che utilizza il server di livello intermedio.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [Informazioni di riferimento sull'API del driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
