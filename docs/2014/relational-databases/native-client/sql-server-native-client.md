---
title: Novità di SQL Server Native Client |&#39;Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62638848"
---
# <a name="what39s-new-in-sql-server-native-client"></a>Novità di SQL Server Native Client&#39;
  Tramite [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] viene installato [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client. Non esistono versioni di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Native Client.  
  
 Non saranno più disponibili aggiornamenti al driver ODBC in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Il successore al driver ODBC in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, denominato [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Windows, viene installato con [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Per ulteriori informazioni su [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC driver 11 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Windows, vedere [Microsoft ODBC driver 11 for SQL Server-Windows](https://www.microsoft.com/download/details.aspx?id=36434).  
  
 L'ultimo aggiornamento del provider OLE DB in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è stato eseguito in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client. Gli sviluppatori che desiderano utilizzare un provider OLE DB per connettersi alla versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dovranno utilizzare il provider OLE DB fornito con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client.  
  
 Negli argomenti seguenti vengono descritte le nuove funzionalità significative di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   [Supporto SQL Server Native Client per il database locale](features/sql-server-native-client-support-for-localdb.md)  
  
-   [Individuazione dei metadati](features/metadata-discovery.md)  
  
-   [Supporto per UTF-16 in SQL Server Native Client 11.0](features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [Supporto di SQL Server Native Client per il ripristino di emergenza a disponibilità elevata](features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Accesso alle informazioni di diagnostica nel registro eventi estesi](features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
 ODBC in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ora supporta tre funzionalità aggiunte a ODBC standard in Windows 7 SDK:  
  
-   Esecuzione asincrona nelle operazioni correlate alla connessione. Per ulteriori informazioni, vedere [esecuzione asincrona](https://go.microsoft.com/fwlink/?LinkID=191493).  
  
-   Estendibilità del tipo di dati C. Per ulteriori informazioni, vedere [tipi di dati C in ODBC](https://go.microsoft.com/fwlink/?LinkID=191495).  
  
     Per supportare questa funzionalità in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client, SQLGetDescField può restituire `SQL_C_SS_TIME2` (per `time` i tipi) `SQL_C_SS_TIMESTAMPOFFSET` o ( `datetimeoffset`per) invece `SQL_C_BINARY`di, se l'applicazione usa ODBC 3,8. Per ulteriori informazioni, vedere [supporto del tipo di dati per i miglioramenti di data e ora ODBC](features/date-and-time-improvements.md).  
  
-   Chiamata di `SQLGetData` con un buffer di piccole dimensioni più volte per recuperare un valore di parametro di grandi dimensioni. Per altre informazioni, vedere [recupero di parametri di output tramite SQLGetData](https://go.microsoft.com/fwlink/?LinkID=191494).  
  
 Negli argomenti seguenti vengono descritte le modifiche nel comportamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   Quando si `ICommandWithParameters::SetParameterInfo`chiama, il valore passato al parametro *pwszName* deve essere un identificatore valido. Per ulteriori informazioni, vedere [ICommandWithParameters](../native-client-ole-db-interfaces/icommandwithparameters.md).  
  
-   Tramite `SQLDescribeParam` viene restituito ora in modo coerente un valore conforme alla specifica ODBC. Per ulteriori informazioni, vedere [SQLDescribeParam](../native-client-odbc-api/sqldescribeparam.md).  
  
-   [Modifica del comportamento del driver ODBC quando si gestiscono le conversioni di caratteri](features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Funzionalità di SQL Server Native Client](features/sql-server-native-client-features.md)  
  
  
