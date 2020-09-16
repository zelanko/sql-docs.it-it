---
description: Metodo position (byte, long)
title: Metodo position (byte, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (byte[], long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 787412c2-4342-49c8-9ca2-7a9ddcd3277c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81248632dfff287d349a627dd4a82499e80d1d64
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433063"
---
# <a name="position-method-byte-long"></a>Metodo position (byte, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce la posizione di un modello specificato nell'oggetto BLOB in base al modello di matrice **byte** e all'indice iniziale specificati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public long position(byte[] bPattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parametri  
 *bPattern*  
  
 Modello da cercare.  
  
 *start*  
  
 Indice iniziale in corrispondenza del quale eseguire la ricerca.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **long** della posizione in cui è stato rilevato il modello o -1 se non è stato rilevato.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo position viene specificato dal metodo position nell'interfaccia java.sql.Blob.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo position &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [Metodi di SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membri di SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
