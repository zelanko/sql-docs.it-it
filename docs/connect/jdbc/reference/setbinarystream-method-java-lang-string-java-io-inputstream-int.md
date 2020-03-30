---
title: Metodo setBinaryStream per il flusso di input - long | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 567297bf-5bec-46ae-8264-29639b9b4a06
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2020b147b67557417b7c64cc05a053f9650d828
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67975168"
---
# <a name="setbinarystream-method--javalangstring-javaioinputstream-int"></a>Metodo setBinaryStream (java.lang.String, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul flusso di input specificato, che conterrà il numero specificato di byte.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setBinaryStream(java.lang.String parameterName,  
                            java.io.InputStream value,  
                            int length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *parameterName*  
  
 Una **stringa** che contiene il nome del parametro.  
  
 *value*  
  
 Oggetto InputStream.  
  
 *length*  
  
 Valore **int** che indica la lunghezza espressa in numero di byte.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo setBinaryStream viene specificato dal metodo setBinaryStream nell'interfaccia java.sql.CallableStatement.  
  
 Se la lunghezza del flusso è diversa da quanto specificato nel parametro *length*, il driver JDBC genera un'eccezione al momento dell'aggiornamento o dell'inserimento della riga.  
  
 Se la lunghezza del flusso è sconosciuta, il parametro *length* può essere impostato su -1 a indicare che il driver deve accettare il flusso indipendentemente dalla lunghezza. Con sqljdbc4.jar, si consiglia di utilizzare il metodo [setBinaryStream Method (java.lang.String, java.io.InputStream)](../../../connect/jdbc/reference/setbinarystream-method-java-lang-string-java-io-inputstream.md) di JDBC 4.0 se nell'applicazione è richiesto l'aggiornamento della colonna da un flusso la cui lunghezza è sconosciuta.  
  
## <a name="see-also"></a>Vedere anche  
 [setBinaryStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)   
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
