---
title: Metodo getPropertyInfo (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.getPropertyInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b5eaad8a-31ef-44ac-af11-d5caa13ac3e2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 946bcde93c9f024d921322b0d84b0ad162aec66d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66785025"
---
# <a name="getpropertyinfo-method-sqlserverdriver"></a>Metodo getPropertyInfo (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Consente di individuare le proprietà necessarie per eseguire la connessione a un database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.sql.DriverPropertyInfo[] getPropertyInfo(java.lang.String Url,  
                                                     java.util.Properties Info)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Url*  
  
 Valore **String** contenente l'URL usato per la connessione al database.  
  
 *info*  
  
 Elenco di coppie di valori delle proprietà, Null al primo utilizzo.  
  
## <a name="return-value"></a>Valore restituito  
 Una matrice di oggetti DriverPropertyInfo.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getPropertyInfo viene specificato dal metodo getPropertyInfo nell'interfaccia Java.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Membri di SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Classe SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
