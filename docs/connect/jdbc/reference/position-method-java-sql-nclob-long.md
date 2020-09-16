---
description: Metodo position (java.sql.NClob, long)
title: Metodo position (java.sql.NClob, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f2354278-d128-4cf4-a170-22c05fcb763b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e810a05d5c289babe665a398f27a670349c2b304
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433013"
---
# <a name="position-method-javasqlnclob-long"></a>Metodo position (java.sql.NClob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la posizione del carattere in corrispondenza della quale viene visualizzato l'oggetto **NClob** specificato *searchstr* nell'oggetto **NClob**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
long position(java.sql.NClob searchstr,  
              long start)  
```  
  
#### <a name="parameters"></a>Parametri  
 *searchstr*  
  
 Oggetto NClob da cercare.  
  
 *start*  
  
 Posizione da cui iniziare la ricerca. La prima posizione è 1.  
  
## <a name="return-value"></a>Valore restituito  
 Posizione in cui viene visualizzata la sottostringa oppure -1 se non è presente. La prima posizione è 1.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo position viene specificato dal metodo position nell'interfaccia java.sql.NClob.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo position &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [Metodi di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membri di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
