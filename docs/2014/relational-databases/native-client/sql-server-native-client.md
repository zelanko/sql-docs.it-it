---
title: Cosa&#39;s New in SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2a01b9d9d13bf5e9135d287553beb8b87c2dcd5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62638848"
---
# <a name="what39s-new-in-sql-server-native-client"></a>Cosa&#39;s New in SQL Server Native Client
  Tramite [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] viene installato [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client. Non esistono versioni di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Native Client.  
  
 Non saranno più disponibili aggiornamenti al driver ODBC in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Il successore al driver ODBC in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, denominato [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Windows, viene installato con [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Per altre informazioni sul [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Windows, vedere [Microsoft ODBC Driver 11 for SQL Server - Windows](https://www.microsoft.com/download/details.aspx?id=36434).  
  
 L'ultimo aggiornamento del provider OLE DB in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è stato eseguito in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client. Gli sviluppatori che desiderano utilizzare un provider OLE DB per connettersi alla versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dovranno utilizzare il provider OLE DB fornito con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client.  
  
 Negli argomenti seguenti vengono descritte le nuove funzionalità significative di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   [Supporto di SQL Server Native Client per Local DB](features/sql-server-native-client-support-for-localdb.md)  
  
-   [Individuazione dei metadati](features/metadata-discovery.md)  
  
-   [Supporto di UTF-16 in SQL Server Native Client 11.0](features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [Supporto di SQL Server Native Client per il ripristino di emergenza a disponibilità elevata](features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Accesso alle informazioni di diagnostica nel log degli eventi estesi](features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
 ODBC in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ora supporta tre funzionalità aggiunte a ODBC standard in Windows 7 SDK:  
  
-   Esecuzione asincrona nelle operazioni correlate alla connessione. Per altre informazioni, vedere [esecuzione asincrona](https://go.microsoft.com/fwlink/?LinkID=191493).  
  
-   Estendibilità del tipo di dati C. Per altre informazioni, vedere [tipi di dati C in ODBC](https://go.microsoft.com/fwlink/?LinkID=191495).  
  
     Per supportare questa funzionalità in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, può restituire SQLGetDescField `SQL_C_SS_TIME2` (per `time` tipi) o `SQL_C_SS_TIMESTAMPOFFSET` (per `datetimeoffset`) invece di `SQL_C_BINARY`, se l'applicazione utilizza ODBC 3.8. Per altre informazioni, vedere [supporto dei tipi di dati per ODBC Date e miglioramenti per la fase](features/date-and-time-improvements.md).  
  
-   Chiamata di `SQLGetData` con un buffer di piccole dimensioni più volte per recuperare un valore di parametro di grandi dimensioni. Per altre informazioni, vedere [recupero di parametri di Output tramite SQLGetData](https://go.microsoft.com/fwlink/?LinkID=191494).  
  
 Negli argomenti seguenti vengono descritte le modifiche nel comportamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   Quando si chiama `ICommandWithParameters::SetParameterInfo`, il valore passato per il *pwszName* parametro deve essere un identificatore valido. Per altre informazioni, vedere [ICommandWithParameters](../native-client-ole-db-interfaces/icommandwithparameters.md).  
  
-   Tramite `SQLDescribeParam` viene restituito ora in modo coerente un valore conforme alla specifica ODBC. Per altre informazioni, vedere [SQLDescribeParam](../native-client-odbc-api/sqldescribeparam.md).  
  
-   [Modifica del comportamento del driver ODBC quando si gestiscono le conversioni di caratteri](features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](features/sql-server-native-client-features.md)  
  
  
