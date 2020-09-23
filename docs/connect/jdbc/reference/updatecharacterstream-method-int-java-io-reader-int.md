---
description: Metodo updateCharacterStream (int, java.io.Reader, int)
title: Metodo updateCharacterStream (int, java.io.Reader, int)
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateCharacterStream (int, java.io.Reader, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b692c372-f6d7-4528-9c5d-cd8421bdb12e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 29d660a9bc91cc37e3882aa7f9ae025a84c65f4e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458013"
---
# <a name="updatecharacterstream-method-int-javaioreader-int"></a>Metodo updateCharacterStream (int, java.io.Reader, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aggiorna la colonna designata con un valore del flusso di caratteri, che conterrà il numero specificato di caratteri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader readerValue,  
                                  int length)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnIndex*  
  
 Valore **int** che indica l'indice di colonna.  
  
 *readerValue*  
  
 Oggetto Reader.  
  
 *length*  
  
 Valore **int** che indica la lunghezza del flusso.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo updateCharacterStream viene specificato dal metodo updateCharacterStream nell'interfaccia java.sql.ResultSet.  
  
 Questo metodo passa caratteri Unicode da un oggetto Reader alle colonne di testo e binarie selezionate. Include tutte le colonne di testo e le colonne **binary**, **varbinary**, **varbinary(max)** , **image** e **xml**, ma non le colonne **udt**.  
  
 Se la lunghezza del flusso è diversa da quella specificata nel parametro *length*, il driver JDBC genera un'eccezione al momento dell'aggiornamento o dell'inserimento della riga.  
  
 Se la lunghezza del flusso è sconosciuta, il parametro *length* può essere impostato su -1 a indicare che il driver deve accettare il flusso indipendentemente dalla lunghezza. Con sqljdbc4.jar, è consigliabile usare il metodo [updateCharacterStream &#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-int-java-io-reader.md) di JDBC 4.0 se l'applicazione vuole aggiornare la colonna da un flusso la cui lunghezza è sconosciuta.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo updateCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
