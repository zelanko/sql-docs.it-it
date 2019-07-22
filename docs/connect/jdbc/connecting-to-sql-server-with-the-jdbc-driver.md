---
title: Connessione a SQL Server con il driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1b88d1824564a9b4fdd3d5340575a5afdff5ca3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956828"
---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>Connessione a SQL Server con il driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Una delle operazioni più importanti che è possibile eseguire con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è la creazione di una connessione a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ogni interazione con il database viene eseguita mediante l'oggetto [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) e poiché il driver JDBC ha un'architettura flat, quasi tutte le operazioni determinanti interessano l'oggetto SQLServerConnection.  
  
 Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in attesa solo su una porta IPv6, impostare la proprietà di sistema java.net.preferIPv6Addresses per assicurarsi che venga usato IPv6 anziché IPv4 per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```java
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 Gli argomenti di questa sezione descrivono come creare e usare una connessione in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Costruzione dell'URL di connessione](../../connect/jdbc/building-the-connection-url.md)|Descrive come creare un URL di connessione per la connessione a un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Illustra anche la connessione a istanze denominate di un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md)|Descrive le varie proprietà di connessione e il loro uso durante la connessione a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Impostazione delle proprietà delle origini dei dati](../../connect/jdbc/setting-the-data-source-properties.md)|Viene descritto come utilizzare le origini dei dati in un ambiente Java EE (Java Platform, Enterprise Edition).|  
|[Uso di una connessione](../../connect/jdbc/working-with-a-connection.md)|Descrive le diverse modalità di creazione di un'istanza della connessione a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Uso del pool di connessioni](../../connect/jdbc/using-connection-pooling.md)|Viene descritto come il driver JDBC supporta l'utilizzo del pool di connessioni.|  
|[Uso del mirroring del database &#40;JDBC&#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|Viene descritto il supporto del driver JDBC per l'utilizzo del mirroring del database.|  
|[Supporto del driver JDBC per disponibilità elevata e ripristino di emergenza](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|Viene descritto come sviluppare un'applicazione che verrà connessa a un gruppo di disponibilità AlwaysOn.|  
|[Uso dell'autenticazione integrata Kerberos per la connessione a SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|Descrive un'implementazione Java per la connessione di applicazioni a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite l'autenticazione integrata Kerberos.|  
|[Connessione a un database SQL di Azure](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|Vengono descritti i problemi di connettività per i database in SQL Azure.|  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
