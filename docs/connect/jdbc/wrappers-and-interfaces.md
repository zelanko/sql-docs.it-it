---
title: Wrapper e interfacce | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3a74f5ccd8a36527dd7c37fc02150d11be632ba9
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025586"
---
# <a name="wrappers-and-interfaces"></a>Wrapper e interfacce

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] supporta le interfacce che consentono la creazione di un proxy di una classe e i wrapper che consentono di accedere alle estensioni dell'API JDBC specifiche di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] tramite un'interfaccia proxy.

## <a name="wrappers"></a>Wrapper

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] supporta l'interfaccia java.sql.Wrapper. Tale interfaccia fornisce un meccanismo per accedere alle estensioni dell'API JDBC specifiche di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] tramite un'interfaccia proxy.

L'interfaccia java. SQL. wrapper definisce due metodi: **isWrapperFor** e **Unwrap**. Il metodo **isWrapperFor** verifica se l'oggetto di input specificato implementa questa interfaccia. Il metodo **unwrap** restituisce un oggetto che implementa questa interfaccia per consentire l'accesso ai metodi specifici di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].

i metodi **isWrapperFor** e **unwrap** vengono esposti come segue:

- [Metodo isWrapperFor &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)

- [Metodo unwrap &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)

- [Metodo isWrapperFor &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)

- [Metodo unwrap &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)

- [Metodo isWrapperFor &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)

- [Metodo &#40;Unwrap SQLServerDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)

- [Metodo isWrapperFor &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)

- [Metodo unwrap &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)

- [Metodo isWrapperFor &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)

- [Unwrap ( &#40;metodo SQLServerStatement)&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)

- [Metodo isWrapperFor &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)

- [Metodo &#40;Unwrap SQLServerXADataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)

## <a name="interfaces"></a>Interfacce

A partire dalla versione 3.0 del driver JDBC per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sono disponibili interfacce che consentono a un server applicazioni di accedere a un metodo specifico del driver dalla classe associata. Il wrapping della classe può essere eseguito dal server applicazioni tramite la creazione di un proxy, esponendo la funzionalità specifica di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] da un'interfaccia. Il driver [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] supporta le interfacce che includono costanti e metodi specifici di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], per consentire a un server applicazioni di creare un proxy della classe.

Le interfacce derivano da interfacce Java standard ed è pertanto possibile utilizzare lo stesso oggetto dopo averne annullato il wrapping per accedere alla funzionalità specifica del driver o alla funzionalità generica di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].

Sono aggiunte le interfacce seguenti:

- [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)

- [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)

- [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)

- [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)

- [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)

- [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)

## <a name="example"></a>Esempio

### <a name="description"></a>Descrizione

In questo esempio viene illustrato come accedere a una funzione specifica di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] da un oggetto DataSource. Il wrapping della classe DataSource potrebbe essere stato eseguito da un server applicazioni. Per accedere alla costante o alla funzione specifica del driver JDBC è possibile annullare il wrapping dall'origine dei dati a un'interfaccia ISQLServerDataSource e utilizzare le funzioni dichiarate in questa interfaccia.

### <a name="code"></a>codice

```java
import javax.sql.*;  
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  

public class UnWrapTest {  
   public static void main(String[] args) {  
      // This is a test.  This DataSource object could be something from an appserver
      // which has wrapped the real SQLServerDataSource with its own wrapper  
      SQLServerDataSource ds = new SQLServerDataSource();  
      checkSendStringParametersAsUnicode(ds);  
   }  

   // Unwrap to the ISQLServerDataSource interface to access the getSendStringParametersAsUnicode function  
   static void checkSendStringParametersAsUnicode(DataSource ds) {  
      try {  
         final ISQLServerDataSource sqlServerDataSource = ds.unwrap(ISQLServerDataSource.class);  
         boolean sendStringParametersAsUnicode = sqlServerDataSource.getSendStringParametersAsUnicode();  

         System.out.println("Send string as parameter value is:-" + sendStringParametersAsUnicode);  

      } catch (SQLException sqlE) {  
         System.out.println("Exception:-" + sqlE);  
      }  
   }  
}  
```

## <a name="see-also"></a>Vedere anche

[Informazioni sui tipi di dati del driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
