---
title: Metodo getBytes (SQLServerBlob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea1b810-b5c1-466d-bdc4-561468214632
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00ae9db184a8fa8818f93402551a58580a9b833b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921589"
---
# <a name="getbytes-method-sqlserverblob"></a>Metodo getBytes (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ottiene i dati BLOB come matrice di byte.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public byte[] getBytes(long pos,  
                       int length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *pos*  
  
 Posizione di inizio, a partire da 1 (non 0).  
  
 *length*  
  
 Lunghezza dei dati da ottenere.  
  
## <a name="return-value"></a>Valore restituito  
 Matrice di **byte** contenente i dati richiesti.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getBytes viene specificato dal metodo getBytes nell'interfaccia java.sql.Blob.  
  
 Se è presente un BLOB Null o di lunghezza zero e si prova a ottenere esattamente zero byte in corrispondenza della posizione 1, viene restituita una matrice di **byte** vuota (matrice di byte di lunghezza 0).  
  
 Se si dispone di una lunghezza BLOB Null o zero e si tenta di ottenere una qualsiasi lunghezza di byte in una posizione diversa da 1, verrà generata un'eccezione di posizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membri di SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
