---
description: Metodo isWrapperFor (SQLServerConnectionPoolDataSource)
title: Metodo isWrapperFor (SQLServerConnectionPoolDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 09ed10eb-6e46-437b-a7c0-3c55574aad38
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d307f92f9711f2ed799b457b03d56afdf23af8f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433333"
---
# <a name="iswrapperfor-method-sqlserverconnectionpooldatasource"></a>Metodo isWrapperFor (SQLServerConnectionPoolDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se questo oggetto è un wrapper per l'interfaccia specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>Parametri  
 *iface*  
  
 Valore **class** che definisce un'interfaccia.  
  
## <a name="return-value"></a>Valore restituito  
 **true** se questo oggetto implementa l'interfaccia o esegue il wrapping di un oggetto che implementa l'interfaccia. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) e il metodo [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) sono definiti dall'interfaccia java.sql.Wrapper, introdotta nella specifica JDBC 4.0.  
  
 Se questo metodo restituisce true, la chiamata a [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) con lo stesso argomento avrà esito positivo.  
  
 Per altre informazioni, vedere [Wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo unwrap &#40;SQLServerConnectionPoolDataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)   
 [Metodi di SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [Membri di SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Classe SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
