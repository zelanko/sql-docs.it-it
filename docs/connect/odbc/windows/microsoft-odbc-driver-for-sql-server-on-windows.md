---
title: Microsoft ODBC Driver for SQL Server in Windows | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c075c7adcc7eeae3ae7a83676256e72b4b86d187
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67989435"
---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server in Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

I driver Microsoft ODBC per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono driver ODBC autonomi che offrono un'API che implementa le interfacce ODBC standard in Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

È possibile usare Microsoft ODBC Driver for SQL Server per creare nuove applicazioni. È anche possibile aggiornare le applicazioni precedenti che attualmente usano un driver ODBC meno recente. ODBC Driver for SQL Server supporta le connessioni a database SQL di Azure, Azure SQL Data Warehouse, SQL Server 2017, SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008 e SQL Server 2005.  

## <a name="summary"></a>Summary

| Versione       | Funzionalità supportate      |
| ------------- |---------------| 
| Microsoft ODBC Driver 17 per SQL Server | <ul><li>Supporto per Always Encrypted per l'API BCP</li><li>Il nuovo attributo della stringa di connessione UseFMTONLY fa in modo che il driver usi metadati legacy in casi particolari in cui sono richieste tabelle temporanee</li>
| Microsoft ODBC Driver 13.1 per SQL Server     | <ul><li>Always Encrypted</li><li>Autenticazione di Azure AD</li><li>Gruppi di disponibilità AlwaysOn</li></ul>   | 
| Microsoft ODBC Driver 13 for SQL Server      | <ul><li>Internationalized Domain Name (IDN)</li></ul> |
| Microsoft ODBC Driver 11 per SQL Server | <ul><li>Pool di connessioni compatibile con il driver</li><li>Resilienza della connessione</li><li>Esecuzione asincrona (metodo di polling)</li></ul> |    

## <a name="documentation"></a>Documentazione  
Questa documentazione per Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] include:  
  
-   [Note sulla versione di ODBC per SQL Server in Windows](../../../connect/odbc/windows/release-notes-odbc-sql-server-windows.md)  
-   [Funzionalità di Microsoft ODBC Driver for SQL Server in Windows](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [Requisiti di sistema, installazione e file del driver](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [Pool di connessioni compatibile con il driver nel driver ODBC per SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [Asynchronous Execution &#40;Notification Method&#41; Sample (Esempio di esecuzione asincrona - metodo di notifica)](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Resilienza di connessione nel driver ODBC di Windows](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [Using Always Encrypted with the ODBC Driver](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) (Utilizzo di Always Encrypted con il driver ODBC)
-   [Uso di Azure Active Directory con ODBC Driver](../../../connect/odbc/using-azure-active-directory.md) 
-   [Uso della stringa di connessione TransparentNetworkIPResolution](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>Community  
- [Blog del team di Microsoft ODBC Driver for SQL Server](https://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [Forum di accesso ai dati di SQL Server](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>Vedere anche  
- [Informazioni su SQL Server Native Client](https://msdn.microsoft.com/sqlserver/ff658532.aspx)   
- [Compilazione di applicazioni con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [Domande frequenti su SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937707.aspx)   
- [Guida di riferimento per programmatori ODBC](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
