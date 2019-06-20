---
title: Metodo getCharacterStream (long, long) (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5a8028bc-c877-4668-b662-0746d462040e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 96fbaf14a04203e08c620b5173bcc2df6d03cb7c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66784951"
---
# <a name="getcharacterstream-method-long-long-sqlservernclob"></a>Metodo getCharacterStream (long, long) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera i dati **NCLOB** come oggetto **Reader** o come flusso di caratteri con una posizione e una lunghezza specificate.  
  
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
 Oggetto Reader contenente i dati **NCLOB**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getCharacterStream viene specificato dal metodo nell'interfaccia java.sql.NClob getCharacterStream.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getCharacterStream &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)   
 [Metodi di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membri di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
