---
description: Metodo getPropertyInfo (SQLServerDriver)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cfdcc8917d818ff74d5897e9481f829f1284bdee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434923"
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
  
 *Info*  
  
 Elenco di coppie di valori delle proprietà, Null al primo utilizzo.  
  
## <a name="return-value"></a>Valore restituito  
 Matrice di oggetti DriverPropertyInfo.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getPropertyInfo viene specificato dal metodo getPropertyInfo nell'interfaccia java.sql.Driver.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Membri di SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Classe SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
