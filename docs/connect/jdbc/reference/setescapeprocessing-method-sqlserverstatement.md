---
title: Metodo setEscapeProcessing (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setEscapeProcessing
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6ac0682e-e04c-4fdb-893b-92408d42051e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ddd79fe975905baa5fb8cab945d6069be611adc3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802974"
---
# <a name="setescapeprocessing-method-sqlserverstatement"></a>Metodo setEscapeProcessing (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta la modalità di elaborazione di escape.  
  
> [!NOTE]  
>  L'elaborazione delle sequenze di escape per [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] è sempre abilitata. L'impostazione di questo metodo su false non ha effetti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setEscapeProcessing(boolean enable)  
```  
  
#### <a name="parameters"></a>Parametri  
 *enable*  
  
 **true** per abilitare l'elaborazione di escape. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setEscapeProcessing viene specificato dal metodo setEscapeProcessing nell'interfaccia Statement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
