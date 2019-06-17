---
title: Metodo setCharacterStream (int, java.io.Reader, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 139a5b74-8d7d-41cf-991a-a142349c58f6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 18e05d4707977499cff3864cef34e39f1bd45feb
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797594"
---
# <a name="setcharacterstream-method-int-javaioreader-int"></a>Metodo setCharacterStream (int, java.io.Reader, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sull'oggetto Reader specificato, che contiene il numero specificato di caratteri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setCharacterStream(int n,  
                                     java.io.Reader reader,  
                                     int length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *n*  
  
 Valore **int** che indica il numero di parametro.  
  
 *reader*  
  
 Oggetto lettore.  
  
 *length*  
  
 Numero di caratteri.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setCharacterStream viene specificato dal metodo setCharacterStream nell'interfaccia PreparedStatement.  
  
 Se la lunghezza del flusso è diversa da quella specificata nel parametro *length*, il driver JDBC genera un'eccezione al momento dell'aggiornamento o dell'inserimento della riga.  
  
 Se la lunghezza del flusso è sconosciuta, il parametro *length* può essere impostato su -1 a indicare che il driver deve accettare il flusso indipendentemente dalla lunghezza. Con sqljdbc4.jar, è consigliabile usare il [metodo setCharacterStream &#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/setcharacterstream-method-int-java-io-reader.md) di JDBC 40 se nell'applicazione è richiesto l'aggiornamento della colonna da un flusso la cui lunghezza è sconosciuta.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
