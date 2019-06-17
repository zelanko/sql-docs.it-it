---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4f7959476f092389f22f2d7720927907b8f59d69
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66771350"
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
  
## <a name="remarks"></a>Remarks  
 Questo metodo getPrecision viene specificato dal metodo getPrecision nell'interfaccia parametermetadata.  
  
 Per i tipi numerici, questo metodo ottiene il numero di cifre decimali. Per i tipi carattere, ottiene la lunghezza massima in caratteri. Per i tipi binari, ottiene la lunghezza massima in byte. Se il numero di cifre è sconosciuto, questo metodo restituisce "0".  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Membri di SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Classe SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
