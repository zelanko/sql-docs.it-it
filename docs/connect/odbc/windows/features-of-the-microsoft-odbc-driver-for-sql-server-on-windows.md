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
author: v-makouz
ms.author: genemi
ms.openlocfilehash: 6e3f7929c17b161d3534474d3d9ad99e559714d2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "69653801"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Funzionalità di Microsoft ODBC Driver for SQL Server in Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-174-for-sql-server-on-windows"></a>Microsoft ODBC Driver 17.4 for SQL Server in Windows

ODBC Driver 17.4 include la possibilità di modificare le impostazioni keep-alive TCP. È possibile modificare le impostazioni aggiungendo valori alle chiavi del Registro di sistema del driver o del DSN. Le chiavi si trovano in `HKEY_LOCAL_MACHINE\Software\ODBC\` per le origini dati di sistema e in `HKEY_CURRENT_USER\Software\ODBC\` per le origini dati utente. Per il DSN è necessario aggiungere i valori in `...\Software\ODBC\ODBC.INI\<DSN Name>` e per il driver in `...\Software\ODBC\ODBCINST.INI\ODBC Driver 17 for SQL Server`.

Per altre informazioni, vedere [Voci del Registro di sistema per i componenti ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md).

I valori sono `REG_SZ` e sono i seguenti:

- `KeepAlive` determina la frequenza dei tentativi effettuati da TCP per verificare l'integrità di una connessione inattiva inviando un pacchetto keep-alive. Il valore predefinito è 30 secondi.

- `KeepAliveInterval` determina l'intervallo tra le ritrasmissioni keep-alive finché non viene ricevuta una risposta. Il valore predefinito è 1 secondo.



## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 for SQL Server in Windows

ODBC Driver 13.1 per SQL Server contiene tutte le funzionalità della versione precedente (11) e aggiunge il supporto di Always Encrypted e dell'autenticazione di Azure Active Directory quando viene usato con Microsoft SQL Server 2016.  
  
Always Encrypted consente ai client di eseguire la crittografia dei dati sensibili all'interno delle applicazioni client e non rivelare le chiavi di crittografia di SQL Server. Un driver abilitato Always Encrypted installato nel computer client fa tutto questo eseguendo automaticamente la crittografia e la decrittografia dei dati sensibili nell'applicazione client di SQL Server. Il driver esegue la crittografia dei dati in colonne riservate prima di passare i dati a SQL Server e riscrive automaticamente le query in modo da mantenere la semantica per l'applicazione. Analogamente, il driver esegue in modo trasparente la decrittografia dei dati archiviati in colonne crittografate del database contenute nei risultati della query. Per altre informazioni, vedere [Using Always Encrypted with the Windows ODBC Driver](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) (Uso di Always Encrypted with the con il driver ODBC di Windows).
 
Azure Active Directory consente a utenti, DBA e programmatori di applicazioni di usare l'autenticazione di Azure Active Directory come meccanismo di connessione al database SQL di Microsoft Azure e a Microsoft SQL Server 2016 tramite le identità di Azure Active Directory (Azure AD). Per altre informazioni, vedere [Uso di Azure Active Directory con il driver ODBC](../../../connect/odbc/using-azure-active-directory.md) e [Connessione al database SQL di Azure o SQL Data Warehouse tramite l'autenticazione di Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Microsoft ODBC Driver 11 for SQL Server in Windows  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contiene tutte le funzionalità del driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client fornito con [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Per altre informazioni, vedere [Programmazione in SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md). Il driver ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è basato sul driver ODBC fornito con il sistema operativo Windows. Per altre informazioni, vedere [Windows Data Access Components SDK](https://msdn.microsoft.com/library/aa968814(VS.85).aspx).  
  
Questa versione del driver ODBC per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contiene le nuove funzionalità seguenti:  
  
### <a name="bcpexe--l-option-for-specifying-a-login-timeout"></a>opzione -l di bcp.exe per la specifica del timeout di accesso
 
L'opzione -l specifica il numero di secondi che devono trascorrere prima che si verifichi il timeout di un accesso `bcp.exe` a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando si prova la connessione a un server. Il timeout di accesso predefinito è di 15 secondi. Il valore del timeout deve essere un numero compreso tra 0 e 65534. Se il valore specificato non è numerico o non è compreso in tale intervallo, `bcp.exe` genera un messaggio di errore. Il valore 0 specifica un timeout infinito. Un timeout di accesso inferiore a (circa) 10 secondi non è affidabile.  
  
### <a name="driver-aware-connection-pooling"></a>Pool di connessioni compatibile con il driver  
Il driver ODBC per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta il [pool di connessioni compatibile con il driver](https://msdn.microsoft.com/library/hh405031(VS.85).aspx). Per altre informazioni, vedere [Pool di connessioni compatibile con il driver nel driver ODBC per SQL Server | Microsoft Docs](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).  
  
### <a name="asynchronous-execution-notification-method"></a>Esecuzione asincrona (metodo di notifica)  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta l'[esecuzione asincrona (metodo di notifica)](https://msdn.microsoft.com/library/hh405038(VS.85).aspx). Per un esempio d'uso, vedere [Asynchronous Execution &#40;Notification Method&#41; Sample](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md) (Esempio di esecuzione asincrona - metodo di notifica).  
  
### <a name="connection-resiliency"></a>Resilienza della connessione
Per garantire che le applicazioni rimangano connesse a un database SQL di Microsoft Azure, il driver ODBC in Windows può ripristinare le connessioni inattive. Per altre informazioni, vedere [Resilienza di connessione nel driver ODBC di Windows](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md).  
  
## <a name="behavior-changes"></a>Differenze di funzionamento

In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client l'opzione `-y0` per `sqlcmd.exe` causava il troncamento dell'output a 1 MB se la larghezza di visualizzazione era 0.
  
A partire da ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], non esiste limite alla quantità di dati recuperabili in un'unica colonna quando è specificato `-y0`. `sqlcmd.exe` ora trasmette colonne di dimensioni pari a 2 GB (massimo per il tipo di dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
Un'altra differenza risiede nel fatto che la specifica di `-h` e `-y0` produce ora un errore che segnala che le opzioni sono incompatibili. `-h`, che specifica il numero di righe da stampare tra le intestazioni di colonna e che non è mai stato compatibile con `-y0`, veniva ignorato anche se non venivano stampate intestazioni.
  
L'opzione `-y0` potrebbe causare gravi problemi a livello di prestazioni del server e della rete, in funzione della dimensione dei dati restituiti.

## <a name="see-also"></a>Vedere anche  
[Microsoft ODBC Driver for SQL Server in Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
