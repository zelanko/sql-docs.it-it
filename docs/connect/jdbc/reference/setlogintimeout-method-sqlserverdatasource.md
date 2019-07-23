---
title: Metodo setLoginTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a64bc643e8d5a9d820b2bcd9cd307f033a869d7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974092"
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>Metodo setLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il numero di secondi di attesa dell'oggetto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) durante il tentativo di stabilire una connessione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>Parametri  
 *loginTimeout*  
  
 Valore **int** che rappresenta il numero di secondi di attesa. Un valore pari a zero indica che il timeout è quello predefinito di sistema, impostato su 15 secondi.  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setLoginTimeout viene specificato dal metodo setLoginTimeout nell'interfaccia javax. SQL. DataSource.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
