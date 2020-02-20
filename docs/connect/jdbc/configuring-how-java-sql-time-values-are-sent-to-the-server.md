---
title: Configurazione della modalità di invio dei valori java.sql.Time al server | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fe6969d51834d0798a530b9cc9926af1b27fec2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028230"
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurazione della modalità di invio dei valori java.sql.Time al server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Se si usa un oggetto java.sql.Time o il tipo JDBC java.sql.Types.TIME per impostare un parametro, è possibile configurare la modalità di invio del valore java.sql.Time al server come tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **time** o come tipo **datetime**.  
  
 Questo scenario si applica quando si utilizza uno dei seguenti metodi:  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 La modalità di invio del valore java.sql.Time può essere configurata tramite la proprietà di connessione **sendTimeAsDatetime**. Per altre informazioni, vedere [Impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Il valore della proprietà di connessione **sendTimeAsDatetime** può essere modificato a livello di codice con [SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Poiché le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] non supportano il tipo di dati **time**, le applicazioni che usano java.sql.Time in genere archiviano i valori java.sql.Time come tipo di dati **datetime** o **smalldatetime** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per usare i tipi di dati **datetime** e **smalldatetime** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando vengono usati valori java.sql.Time, è consigliabile impostare la proprietà di connessione **sendTimeAsDatetime** su **true**. Per usare il tipo di dati **time** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando vengono usati valori java.sql.Time, è consigliabile impostare la proprietà di connessione **sendTimeAsDatetime** su **false**.  
  
 Se si inviano valori java.sql.Time in un parametro il cui tipo di dati può archiviare anche la data, tali date predefinite sono diverse a seconda che il valore java.sql.Time venga inviato come valore **datetime** (1/1/1970) o **time** (1/1/1900). Per altre informazioni sulle conversioni di dati quando si inviano dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Uso di dati relativi a data e ora](https://go.microsoft.com/fwlink/?LinkID=145211).  
  
 Nel driver JDBC Driver 3.0 di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sendTimeAsDatetime** è impostata su true per impostazione predefinita. In una versione successiva la proprietà di connessione **sendTimeAsDatetime** può essere impostata su False per impostazione predefinita.  
  
 Per assicurarsi che l'applicazione continui a funzionare come previsto, indipendentemente dal valore predefinito della proprietà di connessione **sendTimeAsDatetime**, è possibile:  
  
-   Usare java.sql.Time in caso di uso del tipo di dati **time**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usare java.sql.Timestamp quando vengono usati i tipi di dati **datetime**, **smalldatetime** e **datetime2** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
SendTimeAsDatetime deve essere impostata su false per le colonne crittografate poiché le colonne crittografate non supportano la conversione di time in datetime. A partire da Microsoft JDBC Driver 6.0 per SQL Server, la classe SQLServerConnection ha i due metodi seguenti per impostare/ottenere il valore della proprietà sendTimeAsDatetime.

```java
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>Vedere anche
 [Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
