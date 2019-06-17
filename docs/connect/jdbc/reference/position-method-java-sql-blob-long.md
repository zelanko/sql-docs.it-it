---
title: Position (Java, long) (metodo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (java.sql.Blob.long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebd005e5-f6c5-4789-87f9-d2fdacd35060
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e967c02c84943f1fa84eb541cdb28201196a7ce3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802441"
---
# <a name="position-method-javasqlblob-long"></a>Metodo position (java.sql.Blob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce la posizione di un modello specificato nell'oggetto BLOB in base al modello specificato e all'indice iniziale.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public long position(java.sql.Blob pattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parametri  
 *pattern*  
  
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
  
  
