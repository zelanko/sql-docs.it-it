---
title: 'Metodo SQL Server Native Client : Documenti Microsoft'
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
ms.openlocfilehash: 30ef404501c498fca2c722e9eb88bb13997a17b5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305025"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SNAC, o SQL Server Native Client, è un termine che è stato utilizzato in modo intercambiabile per fare riferimento ai driver ODBC e OLE DB per SQL Server.

> [!IMPORTANT] 
> SQL Server Native Client (SQLNCLI) rimane deprecato e non è consigliabile utilizzarlo per le nuove attività di sviluppo. Usare invece il nuovo [Microsoft OLE DB Driver per SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) che verrà aggiornato con le funzionalità server più recenti.

> [!NOTE]
> Per ulteriori informazioni e per scaricare i driver SNAC o ODBC, vedere il post di [blog sul ciclo di vita di SNAC .](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)
> Per ulteriori informazioni sul driver ODBC per SQL Server, vedere [Driver Microsoft ODBC per SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).  

 Informazioni sulle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzionalità di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Native Client rilasciate con , l'ultima versione disponibile di SQL Server Native Client:

-   [Supporto SQL Server Native Client per il database locale](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [Individuazione dei metadati](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [Supporto per UTF-16 in SQL Server Native Client 11.0](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [Supporto di SQL Server Native Client per il ripristino di emergenza a disponibilità elevata](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [Accesso alle informazioni di diagnostica nel registro eventi estesi](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Native Client supporta tre funzionalità che sono state aggiunte a ODBC standard in Windows 7 SDK:  

-   Esecuzione asincrona nelle operazioni correlate alla connessione. Per ulteriori informazioni, vedere [esecuzione asincrona](https://go.microsoft.com/fwlink/?LinkID=191493).  

-   Estendibilità del tipo di dati C. Per ulteriori informazioni, vedere [tipi di dati C in ODBC](https://go.microsoft.com/fwlink/?LinkID=191495).  

     Per supportare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] questa funzionalità in Native Client, SQLGetDescField può restituire **SQL_C_SS_TIME2** (per i tipi **di ora)** o **SQL_C_SS_TIMESTAMPOFFSET** (per **datetimeoffset**) anziché **SQL_C_BINARY**, se l'applicazione utilizza ODBC 3.8. Per ulteriori informazioni, vedere [Supporto dei tipi di dati per miglioramenti](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)di data e ora ODBC .  

-   Chiamata di **SQLGetData** con un buffer di piccole dimensioni più volte per recuperare un valore di parametro di grandi dimensioni. Per ulteriori informazioni, vedere Recupero di parametri di [output tramite SQLGetData](https://go.microsoft.com/fwlink/?LinkID=191494).  

 Negli argomenti seguenti vengono descritte le modifiche nel comportamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  

-   Quando si chiama **ICommandWithParameters::SetParameterInfo**, il valore passato al parametro *pwszName* deve essere un identificatore valido. Per ulteriori informazioni, vedere [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md).  

-   **SQLDescribeParam** restituirà in modo coerente un valore conforme alla specifica ODBC. Per ulteriori informazioni, vedere [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md).  

-   [Modifica del comportamento del driver ODBC quando si gestiscono le conversioni di caratteri](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>Vedere anche  
[Installare SQL Server Native ClientInstall SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [Funzionalità di SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
