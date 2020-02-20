---
title: Metodo getColumnType (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getColumnType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 81815a41-9265-4574-a4d8-f6341a68d9fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80f1177506090d459833f70bdc0b5fdcb115d792
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67952817"
---
# <a name="getcolumntype-method-sqlserverresultsetmetadata"></a>Metodo getColumnType (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il tipo SQL della colonna designata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getColumnType(int column)  
```  
  
#### <a name="parameters"></a>Parametri  
 *column*  
  
 Valore **int** che indica l'indice di colonna.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica il tipo JDBC come definito in java.sql.Types.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getColumnType viene specificato dal metodo getColumnType nell'interfaccia java.sql.ResultSetMetaData.  
  
 Il driver JDBC 3.0 per [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] presenta modifiche funzionali nella colonna DATA_TYPE. Per altre informazioni, vedere [SQLServerDatabaseMetaData.getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
