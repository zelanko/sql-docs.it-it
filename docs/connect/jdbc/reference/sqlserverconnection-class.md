---
title: Classe SQLServerConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e09c80081dc4e3c9230cfba51b1b477420146fb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67971746"
---
# <a name="sqlserverconnection-class"></a>Classe SQLServerConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Rappresenta una connessione JDBC a un database di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Pacchetto:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md), java.io.Serializable  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>Osservazioni  
 SQLServerConnection supporta il pool di connessioni JDBC e può essere una connessione JDBC fisica o logica. SQLServerConnection gestisce il controllo delle transazioni per tutte le istruzioni create e può partecipare alle transazioni distribuite XA gestite tramite un adattatore XAResource.  
  
 SQLServerConnection gestisce un pool di handle delle istruzioni preparate. Tali istruzioni vengono preparate una volta e vengono generalmente eseguite più volte con valori dei dati diversi per i relativi parametri. Le istruzioni preparate vengono gestite anche nelle operazioni di chiusura della connessione logica (in pool).  
  
> [!NOTE]  
>  SQLServerConnection non è thread-safe. Tuttavia, è possibile elaborare contemporaneamente in thread simultanei più istruzioni create da una singola connessione.  
  
 Questa classe supporta l'annullamento del wrapping nella classe SQLServerConnection, l'interfaccia java.sql.Connection e l'interfaccia ISQLServerConnection. Per altre informazioni, vedere [Wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Informazioni di riferimento sull'API del driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
