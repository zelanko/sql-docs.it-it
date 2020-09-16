---
description: Metodo getTrustStore (SQLServerDataSource)
title: Metodo getTrustStore (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7afcb2b9d8402bf1fd8d2f4637488ba8c091f4c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433993"
---
# <a name="gettruststore-method-sqlserverdatasource"></a>Metodo getTrustStore (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il percorso (incluso il nome file) del file trustStore del certificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente il percorso (incluso il nome file) del file trustStore del certificato o Null se non è impostato alcun valore.  
  
## <a name="remarks"></a>Osservazioni  
 Se la proprietà trustStore non è impostata, il metodo [getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md) restituisce Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
