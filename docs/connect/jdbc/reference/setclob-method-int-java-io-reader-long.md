---
description: Metodo setClob (int, java.io.Reader, long)
title: Metodo setClob (int, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 157882dd-1a96-4501-a895-46e88a49266e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5967971a6e7c5c9de773a93695b60ffcbc3d240
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432173"
---
# <a name="setclob-method-int-javaioreader-long"></a>Metodo setClob (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sull'oggetto Reader specificato, che contiene il numero specificato di caratteri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setClob(int parameterIndex,  
                          java.io.Reader reader,  
                          long length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *parameterIndex*  
  
 Valore **int** che specifica l'indice del parametro.  
  
 *reader*  
  
 Oggetto Reader.  
  
 *length*  
  
 Valore **long** che indica il numero di caratteri nel valore del parametro.  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setClob viene specificato dal metodo setClob nell'interfaccia java.sql.PreparedStatement.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo setClob &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)   
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
