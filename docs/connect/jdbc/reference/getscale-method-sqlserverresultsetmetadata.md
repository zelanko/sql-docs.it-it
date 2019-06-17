---
title: Metodo getScale (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getScale
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fe29aa5f-4cc5-413f-8bbd-a58064993d87
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 37fa8f723b9d008651d98e850c794955a54b0c1c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801939"
---
# <a name="getscale-method-sqlserverresultsetmetadata"></a>Metodo getScale (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ottiene il numero di cifre a destra del separatore decimale per la colonna designata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getScale(int column)  
```  
  
#### <a name="parameters"></a>Parametri  
 *column*  
  
 Valore **int** che indica l'indice di colonna.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica la scala della colonna.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getScale viene specificato dal metodo getScale nell'interfaccia ResultSetMetaData.  
  
 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Microsoft JDBC Driver 3.0 include modifiche di comportamento nella colonna DECIMAL_DIGITS. Per altre informazioni, vedere [SQLServerDatabaseMetaData.getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
