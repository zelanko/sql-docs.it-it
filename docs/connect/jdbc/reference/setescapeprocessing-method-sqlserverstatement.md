---
description: Metodo setEscapeProcessing (SQLServerStatement)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8864c591a72fdeabc5dd61ee7df34dcdc5f61c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431903"
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
  
 **true** per abilitare l'elaborazione delle sequenze di escape. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setEscapeProcessing viene specificato dal metodo setEscapeProcessing nell'interfaccia java.sql.Statement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
