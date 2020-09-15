---
description: Metodo truncate (SQLServerClob)
title: Metodo truncate (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.truncate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea3b2a03-387e-49d7-a4d6-ca6a6a354c90
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d25deb243f43b3c4ae4cd82d561e581cc5b5ba95
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431423"
---
# <a name="truncate-method-sqlserverclob"></a>Metodo truncate (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tronca l'oggetto CLOB in base alla lunghezza specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>Parametri  
 *len*  
  
 Lunghezza espressa in caratteri, in base alla quale deve essere troncato l'oggetto CLOB.  
  
## <a name="exceptions"></a>Eccezioni  
 java.sql.SQLException  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo truncate viene specificato dal metodo truncate nell'interfaccia java.sql.Clob.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membri di SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
