---
title: Metodo isWrapperFor (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f77af027-c021-4a17-b264-1ee592bfdd84
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5dbf1b4159d060fce122455436a3ff7b7199e583
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796308"
---
# <a name="iswrapperfor-method-sqlserverdatasource"></a>Metodo isWrapperFor (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se questo oggetto origine dati è un wrapper per l'interfaccia specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>Parametri  
 *iface*  
  
 Oggetto **classe** che definisce un'interfaccia.  
  
## <a name="return-value"></a>Valore restituito  
 **true** se questo oggetto implementa l'interfaccia o esegue il wrapping di un oggetto che implementa l'interfaccia. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Il metodo [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md) e il metodo [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) sono definiti dall'interfaccia java.sql.Wrapper, introdotta nella specifica JDBC 4.0.  
  
 Se questo metodo restituisce true, la chiamata a [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) con lo stesso argomento avrà esito positivo.  
  
 Per altre informazioni, vedere [wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Unwrap &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)   
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
