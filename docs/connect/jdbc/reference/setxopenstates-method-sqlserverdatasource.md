---
description: Metodo setXopenStates (SQLServerDataSource)
title: Metodo setXopenStates (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 345f243f6fb712208df336207ee408cd7596b296
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450613"
---
# <a name="setxopenstates-method-sqlserverdatasource"></a>Metodo setXopenStates (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta un valore **Boolean** che indica se la conversione di stati SQL in stati conformi a XOPEN è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setXopenStates(boolean xopenStates)  
```  
  
#### <a name="parameters"></a>Parametri  
 *xopenStates*  
  
 **true** se la conversione di stati SQL in stati conformi a XOPEN è abilitata. In caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 Se la proprietà xopenStates è impostata su **true**, gli stati SQL vengono convertiti in stati conformi a XOPEN da [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. L'impostazione predefinita è **false** e determina la generazione dei codici di stato SQL 99 da parte del driver JDBC. Se la proprietà xopenStates non è impostata, il metodo [getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md) restituisce il valore predefinito **false**.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
