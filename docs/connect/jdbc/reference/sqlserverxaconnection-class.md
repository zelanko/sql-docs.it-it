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
ms.openlocfilehash: 32d538e31ca3f4a0d9b23411ebcb7b282df46b33
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67970316"
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
  
## <a name="remarks"></a>Osservazioni  
 Un oggetto SQLServerXAConnection può essere integrato in una transazione distribuita tramite un oggetto [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md). Lo strumento di gestione delle transazioni, generalmente parte di un server di livello intermedio, gestisce un oggetto SQLServerXAConnection tramite l'oggetto SQLServerXAResource.  
  
> [!NOTE]  
>  I programmatori di applicazioni in genere non utilizzano direttamente questa interfaccia. Viene utilizzata principalmente da un responsabile transazioni che utilizza il server di livello intermedio.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [Informazioni di riferimento sull'API del driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
