---
title: Metodo setBytes (long, byte, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 271669134e18d3c6040f1e2e10163b5d5e21daab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797605"
---
# <a name="setbytes-method-long-byte-int-int"></a>Metodo setBytes (long, byte, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Scrive tutta o parte della matrice di byte specificata nell'oggetto BLOB a partire dalla posizione, dall'offset e dalla lunghezza specificati; quindi restituisce il numero di byte scritti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes,  
                    int offset,  
                    int len)  
```  
  
#### <a name="parameters"></a>Parametri  
 *pos*  
  
 Posizione (in base 1) nell'oggetto BLOB in corrispondenza della quale iniziare la scrittura dei dati.  
  
 *bytes*  
  
 Matrice di byte da scrivere nell'oggetto BLOB.  
  
 *offset*  
  
 Offset nella matrice di byte in cui iniziare la lettura dei dati dalla matrice **byte**.  
  
 *len*  
  
 Numero di byte di cui tentare la lettura dalla matrice di byte nell'oggetto BLOB.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** contenente il numero di byte scritti.  
  
## <a name="exceptions"></a>Eccezioni  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setBytes viene specificato dal metodo setBytes nell'interfaccia java.sql.Blob.  
  
 I dati vengono sovrascritti a partire dalla posizione specificata e possono superare la lunghezza iniziale dell'oggetto BLOB. Se si specifica un valore posizione+1, verranno aggiunti byte. Se si passa un valore posizione+2 o superiore (o zero o inferiore) verrà generato un errore di posizione. Se si passa una matrice **byte** di lunghezza zero verrà restituito zero in quanto non sono stati scritti byte.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo setBytes &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [Metodi di SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membri di SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
