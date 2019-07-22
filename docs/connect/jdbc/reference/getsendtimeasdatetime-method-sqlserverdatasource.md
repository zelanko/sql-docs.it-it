---
title: Metodo getSendTimeAsDatetime (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e1396ac28a7e41dbf530f7e4a251876f6c340871
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979941"
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>Metodo getSendTimeAsDatetime (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Questo metodo è stato aggiunto in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 Restituisce l'impostazione della proprietà di connessione **sendTimeAsDatetime** .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se i valori java. SQL. Time verranno inviati al server come [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo **DateTime** . **false** se i valori java. SQL. Time verranno inviati al server come [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo **Time** .  
  
## <a name="remarks"></a>Remarks  
 Per ulteriori informazioni sulla proprietà di connessione **sendTimeAsDatetime** , vedere [impostazione delle proprietà di connessione](../../../connect/jdbc/setting-the-connection-properties.md) .  
  
 L'oggetto [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) consente di impostare la proprietà di connessione **sendTimeAsDatetime** a livello di codice.  
  
 Per ulteriori informazioni, vedere [configurazione della modalità di invio dei valori java. SQL. Time al server](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
