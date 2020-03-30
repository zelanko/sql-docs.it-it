---
title: Metodo jdbcCompliant (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.jdbcCompliant
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b299b20d-d1cd-45b3-91dc-dcf579498570
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c36d7980355eed1e1a1e8f42fb53c75fdb70d0ed
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67976952"
---
# <a name="jdbccompliant-method-sqlserverdriver"></a>Metodo jdbcCompliant (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Verifica che [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sia conforme alla specifica JDBC.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean jdbcCompliant()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se il driver JDBC soddisfa i requisiti minimi. In caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo jdbcCompliant viene specificato dal metodo jdbcCompliant nell'interfaccia java.sql.driver.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Membri di SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Classe SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
