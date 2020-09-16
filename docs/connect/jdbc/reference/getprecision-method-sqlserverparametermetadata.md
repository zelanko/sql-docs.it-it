---
description: Metodo getPrecision (SQLServerParameterMetaData)
title: Metodo getPrecision (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getPrecision
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8bd79484-bab6-423b-978f-d7ec7132ebeb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0af3f0f87c32038b8d6b16839993de5ae6aa056
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434953"
---
# <a name="getprecision-method-sqlserverparametermetadata"></a>Metodo getPrecision (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il numero di cifre decimali del parametro designato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getPrecision(int param)  
```  
  
#### <a name="parameters"></a>Parametri  
 *param*  
  
 Valore **int** che indica l'indice del parametro.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica la precisione del parametro designato.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getPrecision viene specificato dal metodo getPrecision nell'interfaccia java.sql.ParameterMetaData.  
  
 Per i tipi numerici, questo metodo ottiene il numero di cifre decimali. Per i tipi carattere, ottiene la lunghezza massima in caratteri. Per i tipi binari, ottiene la lunghezza massima in byte. Se il numero di cifre è sconosciuto, questo metodo restituisce "0".  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Membri di SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Classe SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
