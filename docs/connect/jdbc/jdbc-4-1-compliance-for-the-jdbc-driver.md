---
title: JDBC 4.1 conformità per il Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f087fd40-8451-478e-b465-43112c711515
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7c21c548b113e9da03661ca3beb04b6757c92697
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66781639"
---
# <a name="jdbc-41-compliance-for-the-jdbc-driver"></a>Conformità con JDBC 4.1 per il driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  Le versioni precedenti a Microsoft JDBC Driver 4.2 per SQL Server sono compatibili con le specifiche Java Database Connectivity API 4.0. Questa sezione non è applicabile per le versioni precedenti alla 4.2.  
  
 La specifica Java Database Connectivity API 4.1 è supportata da Microsoft JDBC Driver 4.2 per SQL Server, con i metodi API seguenti.  
  
 **Classe SQLServerConnection**  
  
|Nuovo metodo|Descrizione|Implementazione del driver JDBC|  
|----------------|-----------------|--------------------------------|  
|void abort(Executor executor)|Termina una connessione aperta a SQL Server.|Implementato come descritto nell'interfaccia java.sql.Connection. Per altre informazioni, vedere [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
|void setSchema(String schema)|Imposta lo schema per la connessione corrente.|SQL Server non supporta l'impostazione dello schema per la sessione corrente. Se questo metodo viene chiamato, il driver registra un messaggio di avviso in modo invisibile all'utente. Per altre informazioni, vedere [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
|String getSchema()|Restituisce il nome dello schema per la connessione corrente.|Poiché SQL Server non supporta l'impostazione dello schema per la connessione corrente, il driver restituisce lo schema predefinito dell'utente. Per altre informazioni, vedere [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html).|  
  
 **Classe SQLServerDatabaseMetaData**  
  
|Nuovo metodo|Descrizione|Implementazione del driver JDBC|  
|----------------|-----------------|--------------------------------|  
|boolean generatedKeyAlwaysReturned()|Restituisce true, dal momento che il driver supporta il recupero delle chiavi generate|Implementato come descritto in java.sql. Interfaccia DatabaseMetaData. Per altri dettagli, vedere [java.sql.DatabaseMetaData](https://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html).|  
|ResultSet getPseudoColumns(String catalog, String schemaPattern,String tableNamePattern,String columnNamePattern)|Recupera una descrizione delle pseudocolonne o delle colonne nascoste|Restituisce un set di risultati vuoto, dal momento che SQL Server non dispone di una nozione formale di pseudocolonne. Per altri dettagli, vedere [java.sql.DatabaseMetaData](https://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html).|  
  
 **Classe SQLServerStatement**  
  
|Nuovo metodo|Descrizione|Implementazione del driver JDBC|  
|----------------|-----------------|--------------------------------|  
|void closeOnCompletion()|Specifica che l'istruzione verrà chiusa quando vengono chiusi tutti i relativi set di risultati dipendenti.|Implementato come descritto nell'interfaccia java.sql.Statement. Per altri dettagli, vedere [java.sql.Statement](https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html).|  
|boolean isCloseOnCompletion()|Restituisce un valore che indica se l'istruzione verrà chiusa quando vengono chiusi tutti i relativi set di risultati dipendenti.|Implementato come descritto nell'interfaccia java.sql.Statement. Per altri dettagli, vedere [java.sql.Statement](https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html).|  
  
 La specifica Java Database Connectivity API 4.1 è supportata da Microsoft JDBC Driver 4.2 per SQL Server, con le funzionalità seguenti.  
  
|Nuova funzionalità|Descrizione|  
|-----------------|-----------------|  
|Nuova funzione di escape<br /><br /> Escape di righe restituite limitate|Parzialmente supportato<br /><br /> Sintassi di escape: limite \<righe > [OFFSET < offset_righe >](using-sql-escape-sequences.md).|  
  
 La specifica Java Database Connectivity API 4.1 è supportata da Microsoft JDBC Driver 4.2 per SQL Server, con i mapping dei tipi di dati seguenti.  
  
|Mapping di tipi di dati|Descrizione|  
|------------------------|-----------------|  
|Ora sono supportati nuovi mapping dei tipi di dati nei metodi PreparedStatement.setObject() e PreparedStatement.setNull().|1. Nuovo mapping dei tipi da Java a JDBC<br /><br /> (a) Da java.math.BigInteger a BIGINT JDBC<br /><br /> (b) Da java.util.Date e java.util.Calendar a TIMESTAMP JDBC<br /><br /> 2. Nuove conversioni dei tipi di dati:<br /><br /> (a) Da java.math.BigInteger a CHAR, VARCHAR, LONGVARCHAR e BIGINT<br /><br /> (b) Da java.util.Date e java.util.Calendar a CHAR, VARCHAR, LONGVARCHAR, DATE, TIME e TIMESTAMP<br /><br /> Per ulteriori informazioni, vedere la specifica JDBC 4.1.|  
  
  
