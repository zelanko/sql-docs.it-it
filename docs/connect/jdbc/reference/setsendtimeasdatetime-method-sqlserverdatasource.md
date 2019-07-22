---
title: Metodo setSendTimeAsDatetime (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 293667d8e3e06fb5eda7a74fdeed58c89fb0f1ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972965"
---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>Metodo setSendTimeAsDatetime (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Questo metodo è stato aggiunto in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 Modifica l'impostazione della proprietà di connessione **sendTimeAsDatetime** .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sendTimeAsDateTime*  
  
 Valore booleano. Se true, comporta l'invio dei valori java.sql.Time al server come tipi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime**. Se false, comporta l'invio dei valori java.sql.Time al server come tipi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **time**.  
  
## <a name="remarks"></a>Remarks  
 [SQLServerDataSource. getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md) restituisce l'impostazione della proprietà di connessione **sendTimeAsDatetime** .  
  
 Per ulteriori informazioni sulla proprietà di connessione **sendTimeAsDatetime** , vedere [impostazione delle proprietà di connessione](../../../connect/jdbc/setting-the-connection-properties.md).  
  
 Per ulteriori informazioni, vedere [configurazione della modalità di invio dei valori java. SQL. Time al server](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
