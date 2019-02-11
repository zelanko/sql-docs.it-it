---
title: Funzionalità di Microsoft ODBC Driver for SQL Server in Windows | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db5c3e2e8265e88d49025ffd65894623fc5c5f85
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202240"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Funzionalità di Microsoft ODBC Driver for SQL Server in Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 for SQL Server in Windows

Il Driver ODBC 13.1 per SQL Server contiene tutte le funzionalità della versione precedente (11) e aggiunge il supporto per Always Encrypted e Azure Active Directory l'autenticazione quando usato in combinazione con Microsoft SQL Server 2016.  
  
Always Encrypted consente ai client di eseguire la crittografia dei dati sensibili all'interno delle applicazioni client e non rivelare le chiavi di crittografia di SQL Server. Un driver abilitato Always Encrypted installato nel computer client fa tutto questo eseguendo automaticamente la crittografia e la decrittografia dei dati sensibili nell'applicazione client di SQL Server. Il driver esegue la crittografia dei dati in colonne riservate prima di passare i dati a SQL Server e riscrive automaticamente le query in modo da mantenere la semantica per l'applicazione. Analogamente, il driver esegue in modo trasparente la decrittografia dei dati archiviati in colonne crittografate del database contenute nei risultati della query. Per altre informazioni, vedere [Using Always Encrypted with the Windows ODBC Driver](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) (Uso di Always Encrypted with the con il driver ODBC di Windows).
 
Azure Active Directory consente agli utenti, gli amministratori di database e i programmatori di applicazioni utilizzare l'autenticazione di Azure Active Directory come un meccanismo di connessione al Database SQL di Microsoft Azure e Microsoft SQL Server 2016 tramite identità in Azure Active Directory (Azure AD ). Per altre informazioni, vedere [tramite Azure Active Directory con il Driver ODBC](../../../connect/odbc/using-azure-active-directory.md), e [ci si connette al Database SQL o SQL Data Warehouse da con Azure Active Directory l'autenticazione](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Microsoft ODBC Driver 11 for SQL Server in Windows  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contiene tutte le funzionalità del driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client fornito con [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Per altre informazioni, vedere [Programmazione in SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md). Il driver ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è basato sul driver ODBC fornito con il sistema operativo Windows. Per altre informazioni, vedere [Windows Data Access Components SDK](https://msdn.microsoft.com/library/aa968814(VS.85).aspx).  
  
Questa versione del driver ODBC per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contiene le nuove funzionalità seguenti:  
  
### <a name="bcpexe--l-option-for-specifying-a-login-timeout"></a>opzione -l bcp.exe per specificare un timeout di accesso
 
L'opzione -l specifica il numero di secondi che devono trascorrere prima che si verifichi il timeout di un accesso `bcp.exe` a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando si prova la connessione a un server. Il timeout di accesso predefinito è 15 secondi. Il valore del timeout deve essere un numero compreso tra 0 e 65534. Se il valore specificato non è numerico o non è compreso in tale intervallo, `bcp.exe` genera un messaggio di errore. Un valore pari a 0 specifica un timeout infinito. Un timeout di accesso inferiore a (circa) 10 secondi non è affidabile.  
  
### <a name="driver-aware-connection-pooling"></a>Pool di connessioni compatibile con il driver  
Il driver ODBC per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta il [pool di connessioni compatibile con il driver](https://msdn.microsoft.com/library/hh405031(VS.85).aspx). Per altre informazioni, vedere [Pool di connessioni compatibile con il driver nel driver ODBC per SQL Server | Microsoft Docs](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).  
  
### <a name="asynchronous-execution-notification-method"></a>Esecuzione asincrona (metodo di notifica)  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta l'[esecuzione asincrona (metodo di notifica)](https://msdn.microsoft.com/library/hh405038(VS.85).aspx). Per un esempio d'uso, vedere [Asynchronous Execution &#40;Notification Method&#41; Sample](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md) (Esempio di esecuzione asincrona - metodo di notifica).  
  
### <a name="connection-resiliency"></a>Resilienza della connessione
Per garantire che le applicazioni rimangano connesse a un database SQL di Microsoft Azure, il driver ODBC in Windows può ripristinare le connessioni inattive. Per altre informazioni, vedere [Resilienza di connessione nel driver ODBC di Windows](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md).  
  
## <a name="behavior-changes"></a>Differenze di funzionamento

Nelle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, il `-y0` opzione per `sqlcmd.exe` causato output risulta troncato in corrispondenza di 1 MB se la larghezza di visualizzazione è 0.
  
A partire da ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], non esiste limite alla quantità di dati recuperabili in un'unica colonna quando è specificato `-y0`. `sqlcmd.exe` ora trasmette colonne di dimensioni pari a 2 GB (massimo per il tipo di dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
Un'altra differenza è che se si specifica sia `-h` e `-y0` genera ora un errore di creazione di report, le opzioni sono incompatibili. `-h`, che specifica il numero di righe da stampare tra le intestazioni di colonna e che non è mai stato compatibile con `-y0`, veniva ignorato anche se non venivano stampate intestazioni.
  
L'opzione `-y0` potrebbe causare gravi problemi a livello di prestazioni del server e della rete, in funzione della dimensione dei dati restituiti.

## <a name="see-also"></a>Vedere anche  
[Microsoft ODBC Driver for SQL Server in Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
