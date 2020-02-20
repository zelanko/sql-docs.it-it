---
title: Metodo getCharacterStream (long, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a47b7ea56873b0b502ba39a91e4d1ba30044e993
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953251"
---
# <a name="getcharacterstream-method-long-long"></a>Metodo getCharacterStream (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce i dati **CLOB** come oggetto Reader o come flusso di caratteri con la posizione e la lunghezza specificate.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                         long length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *pos*  
  
 Valore **long** che indica l'offset rispetto al primo carattere del valore parziale da recuperare.  
  
 *length*  
  
 Valore **long** che indica la lunghezza in caratteri del valore parziale da recuperare.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto Reader contenente i dati **Clob**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getCharacterStream viene specificato dal metodo getCharacterStream nell'interfaccia java.sql.Clob.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getCharacterStream &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [Metodi di SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membri di SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  
