---
title: Metodo updateBinaryStream (int, java.io.InputStream, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBinaryStream (int, java.io.InputStream, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c8e55377-aaea-4415-8159-938fab1b2a93
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57cf34cb0ff1071579bdeb97e7b3ce6c095459f2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67985694"
---
# <a name="updatebinarystream-method-int-javaioinputstream-int"></a>Metodo updateBinaryStream (int, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aggiorna la colonna designata con un valore del flusso binario, che conterrà il numero specificato di byte.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void updateBinaryStream(int columnIndex,  
                               java.io.InputStream x,  
                               int length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnIndex*  
  
 Valore **int** che indica l'indice di colonna.  
  
 *x*  
  
 Oggetto InputStream.  
  
 *length*  
  
 Valore **int** che indica la lunghezza del flusso.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo updateBinaryStream viene specificato dal metodo updateBinaryStream nell'interfaccia java.sql.ResultSet.  
  
 Questo metodo passa byte da un oggetto InputStream a colonne binarie di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] selezionate, ad esempio binary, varbinary, varbinary(max), image, xml e udt. L'aggiornamento delle colonne di tipo carattere non è supportato con questo metodo. Per aggiornare le colonne di tipo carattere con un InputStream, usare il metodo [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md).  
  
 Se la lunghezza del flusso è diversa da quella specificata nel parametro *length*, il driver JDBC genera un'eccezione al momento dell'aggiornamento o dell'inserimento della riga.  
  
 Se la lunghezza del flusso è sconosciuta, il parametro *length* può essere impostato su -1 a indicare che il driver deve accettare il flusso indipendentemente dalla lunghezza. Con sqljdbc4.jar, è consigliabile usare il [metodo updateBinaryStream &#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/updatebinarystream-method-int-java-io-inputstream.md) di JDBC 40 se nell'applicazione è richiesto l'aggiornamento della colonna da un flusso la cui lunghezza è sconosciuta.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo updateBinaryStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
