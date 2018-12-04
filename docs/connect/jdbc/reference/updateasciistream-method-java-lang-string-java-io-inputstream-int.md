---
title: Metodo updateAsciiStream (java.io.InputStream, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateAsciiStream (java.lang.String, java.io.InputStream, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4e2997a0-c18e-4114-bce9-0ab4b2b9f92c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a548e0b6beb1815052167d28d67d1228c0bf6dfc
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52517303"
---
# <a name="updateasciistream-method-javalangstring-javaioinputstream-int"></a>Metodo updateAsciiStream (java.lang.String, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aggiorna il nome della colonna designata con un valore del flusso ASCII, che conterrà il numero specificato di byte.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void updateAsciiStream(java.lang.String columnName,  
                              java.io.InputStream x,  
                              int length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnName*  
  
 Valore **String** contenente il nome della colonna.  
  
 *x*  
  
 Un oggetto InputStream.  
  
 *length*  
  
 Valore **int** che indica la lunghezza del flusso.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo updateAsciiStream viene specificato dal metodo updateAsciiStream nell'interfaccia ResultSet.  
  
 Questo metodo passa caratteri ASCII (byte) da un oggetto InputStream a colonne di tipo carattere convertibili, ovvero l'intervallo ASCII [0x00 - 0x7F] di Unicode e le tabelle codici 874, 932, 936 949 e 950 e da 1250 a 1258. Esegue una conversione nella pagina delle regole di confronto di destinazione. Se si tenta di aggiornare una colonna di destinazione non convertibile, verrà generata un'eccezione. Per le colonne binarie, vengono passati byte non elaborati.  
  
 Se la lunghezza del flusso è diversa da quella specificata nel parametro *length*, il driver JDBC genera un'eccezione al momento dell'aggiornamento o dell'inserimento della riga.  
  
 Se la lunghezza del flusso è sconosciuta, il parametro *length* può essere impostato su -1 a indicare che il driver deve accettare il flusso indipendentemente dalla lunghezza. Con sqljdbc4.jar, è consigliabile usare il [metodo updateAsciiStream &#40;java.lang.String, java.io.InputStream&#41;](../../../connect/jdbc/reference/updateasciistream-method-java-lang-string-java-io-inputstream.md) di JDBC 4.0 se nell'applicazione è richiesto l'aggiornamento della colonna da un flusso la cui lunghezza è sconosciuta.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo updateAsciiStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
