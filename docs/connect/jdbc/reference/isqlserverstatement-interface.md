---
title: Interfaccia ISQLServerStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7f83b514-6e76-4f37-baf3-a10db2010e7c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7a49ef95ac7e6ee122252577ccff9ec535c912fe
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796422"
---
# <a name="isqlserverstatement-interface"></a>Interfaccia ISQLServerStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Rappresenta l'implementazione di base della funzionalità dell'istruzione JDBC. Questa interfaccia è stata aggiunta in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 **Pacchetto:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.sql.Statement  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public interface ISQLServerStatement  
```  
  
## <a name="remarks"></a>Remarks  
 Questa interfaccia viene implementata da [classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
 L'interfaccia espone i metodi specifici di [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] seguenti:  
  
|Metodo|Per ulteriori informazioni, vedere|  
|------------|-------------------------------|  
|public String getResponseBuffering|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|  
|public void setResponseBuffering|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di riferimento sull'API del driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
