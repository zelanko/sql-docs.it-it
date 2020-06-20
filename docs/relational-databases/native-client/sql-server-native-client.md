---
title: Informazioni
description: Informazioni sulle funzionalità di SQL Server Native Client (SNAC). SQL Server Native Client si riferisce ai driver ODBC e OLE DB per SQL Server.
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eb9d7878f4edc9f81b7b17b5fdf44da5c9dcec48
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84948665"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SNAC, o SQL Server Native Client, è un termine che è stato usato in modo intercambiabile per fare riferimento ai driver ODBC e OLE DB per SQL Server.

> [!IMPORTANT] 
> Il SQL Server Native Client (SQLNCLI) rimane deprecato e non è consigliabile utilizzarlo per un nuovo lavoro di sviluppo. Usare invece il nuovo [Microsoft OLE DB Driver per SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) che verrà aggiornato con le funzionalità server più recenti.

> [!NOTE]
> Per ulteriori informazioni e per scaricare i driver SNAC o ODBC, vedere il [post di Blog](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)relativo al ciclo di vita di snac.
> Per ulteriori informazioni sul driver ODBC per SQL Server, vedere [Microsoft ODBC driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).  

 Informazioni sulle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzionalità di Native Client rilasciate con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , l'ultima versione disponibile di SQL Server Native Client:

-   [Supporto SQL Server Native Client per il database locale](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [Individuazione dei metadati](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [Supporto per UTF-16 in SQL Server Native Client 11.0](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [Supporto di SQL Server Native Client per il ripristino di emergenza a disponibilità elevata](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [Accesso alle informazioni di diagnostica nel log degli eventi estesi](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

ODBC in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supporta tre funzionalità che sono state aggiunte a ODBC standard in Windows 7 SDK:  

-   Esecuzione asincrona nelle operazioni correlate alla connessione. Per ulteriori informazioni, vedere [esecuzione asincrona](https://go.microsoft.com/fwlink/?LinkID=191493).  

-   Estendibilità del tipo di dati C. Per ulteriori informazioni, vedere [tipi di dati C in ODBC](https://go.microsoft.com/fwlink/?LinkID=191495).  

     Per supportare questa funzionalità in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client, SQLGetDescField può restituire **SQL_C_SS_TIME2** (per i tipi di **ora** ) o **SQL_C_SS_TIMESTAMPOFFSET** (per **DateTimeOffset**) anziché **SQL_C_BINARY**, se l'applicazione usa ODBC 3,8. Per ulteriori informazioni, vedere [supporto del tipo di dati per i miglioramenti di data e ora ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md).  

-   Chiamare **SQLGetData** con un buffer di piccole dimensioni più volte per recuperare un valore di parametro di grandi dimensioni. Per altre informazioni, vedere [recupero di parametri di output tramite SQLGetData](https://go.microsoft.com/fwlink/?LinkID=191494).  

 Negli argomenti seguenti vengono descritte le modifiche nel comportamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  

-   Quando si chiama **ICommandWithParameters::** SetValue, il valore passato al parametro *pwszName* deve essere un identificatore valido. Per ulteriori informazioni, vedere [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md).  

-   **SQLDescribeParam** restituirà in modo coerente un valore conforme a specifiche ODBC. Per ulteriori informazioni, vedere [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md).  

-   [Modifica del comportamento del driver ODBC quando si gestiscono le conversioni di caratteri](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>Vedere anche  
[Installa SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [Funzionalità di SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
