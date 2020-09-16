---
description: Metodo isWrapperFor (SQLServerXADataSource)
title: Metodo isWrapperFor (SQLServerXADataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d612461d-4c3f-46db-b968-ff4c80b2aa7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: caab887a8e104313f78a593520ea7d735008fd1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433293"
---
# <a name="iswrapperfor-method-sqlserverxadatasource"></a>Metodo isWrapperFor (SQLServerXADataSource)
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
 Il metodo [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md) e il metodo [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) sono definiti dall'interfaccia java.sql.Wrapper, introdotta nella specifica JDBC 4.0.  
  
 Se questo metodo restituisce true, la chiamata a [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md) con lo stesso argomento avrà esito positivo.  
  
 Per altre informazioni, vedere [Wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo unwrap &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)   
 [Metodi di SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [Membri di SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [Classe SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
