---
title: I membri di SQLServerNClob | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8386d896391405777648ee3ec27b188b313c737c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66788963"
---
# <a name="sqlservernclob-members"></a>Membri di SQLServerNClob
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Nelle tabelle seguenti sono elencati i membri esposti dalla classe [SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md).  
  
## <a name="constructors"></a>Costruttori  
 Nessuna.  
  
## <a name="fields"></a>Campi  
 Nessuna.  
  
## <a name="inherited-fields"></a>Campi ereditati  
 Nessuna.  
  
## <a name="methods"></a>Metodi  
  
|nome|Descrizione|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|Questo metodo libera l'oggetto **NCLOB** e rilascia le risorse bloccate.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|Recupera le **NCLOB** valore designato dalle **java.sql.NClob** oggetto come flusso ASCII.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|Recupera le **NCLOB** valore designato dalle **java.sql.NClob** oggetto.|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|Recupera una copia della sottostringa specificata nel **NCLOB** valore designato dalle **java.sql.NClob** oggetto.|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|Recupera il numero di caratteri di **NCLOB** valore designato dal **java.sql.NClob** oggetto.|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|Recupera la posizione dei caratteri dell'oggetto **java.sql.NClob** specificato o della sottostringa in **java.sql.NClob** in base alla posizione di inizio specificata.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|Recupera un flusso da usare per scrivere caratteri ASCII nel valore **NCLOB** rappresentato da questo oggetto **java.sql.NClob**, a partire dalla posizione specificata.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|Recupera un flusso da usare per scrivere un flusso di caratteri Unicode nel valore **NCLOB** rappresentato da questo oggetto **java.sql.NClob**, a partire dalla posizione specificata.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|Scrive l'oggetto specificato **stringa** per il **NCLOB** iniziando in corrispondenza della posizione specificata.|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|Tronca il valore **NCLOB** in base alla lunghezza specificata.|  
  
## <a name="inherited-methods"></a>Metodi ereditati  
  
|Classe ereditata da|Metodi|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Clob|free, getAsciiStream, getCharacterStream, getSubString, length, position, setAsciiStream, setCharacterStream, setString, truncate|  
  
## <a name="see-also"></a>Vedere anche  
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
