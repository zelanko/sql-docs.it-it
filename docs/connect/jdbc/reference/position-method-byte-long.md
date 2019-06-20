---
title: Metodo Position (byte, long) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e6056412f6ab2726112d5286f2f52c83ff6691cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802472"
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
  
## <a name="remarks"></a>Remarks  
 Questo metodo di posizione viene specificato dal metodo di posizione nell'interfaccia Java.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Position &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [Metodi di SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membri di SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
