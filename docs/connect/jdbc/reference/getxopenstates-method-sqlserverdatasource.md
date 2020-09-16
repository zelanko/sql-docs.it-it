---
description: Metodo getXopenStates (SQLServerDataSource)
title: Metodo getXopenStates (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de6fdf6b-8345-4490-b35e-7115b61e782e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 654b7a56a98b0a70599e21ef55a12d4db420890d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433713"
---
# <a name="getxopenstates-method-sqlserverdatasource"></a>Metodo getXopenStates (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un valore **booleano** che indica se la conversione di stati SQL in stati conformi a XOPEN è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getXopenStates()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se la conversione di stati SQL in stati conformi a XOPEN è abilitata. In caso contrario, **false**.  
  
## <a name="remarks"></a>Osservazioni  
 Se la proprietà xopenStates è impostata su **true**, gli stati SQL vengono convertiti in stati conformi a XOPEN da [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. L'impostazione predefinita è **false** e determina la generazione dei codici di stato SQL 99 da parte del driver JDBC. Se la proprietà xopenStates non è impostata, il metodo getXopenStates restituisce il valore predefinito **false**.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
