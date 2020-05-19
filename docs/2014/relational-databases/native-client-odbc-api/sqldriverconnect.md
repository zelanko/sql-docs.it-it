---
title: SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5f5ef42a9d04a4d1ae72382f44fdf01b62fc6b14
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706272"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
  Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client definisce attributi di connessione che sostituiscono o migliorano le parole chiave della stringa di connessione. Per diverse parole chiave della stringa di connessione sono disponibili valori predefiniti specificati dal driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Per un elenco delle parole chiave disponibili nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client, vedere [utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Per ulteriori informazioni sugli [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attributi di connessione e sui comportamenti predefiniti del driver, vedere [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
 Per informazioni sulle parole chiave della stringa di connessione valide per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client, vedere [utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Se il `SQLDriverConnect` valore del parametro *DriverCompletion* è SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client recupera i valori delle parole chiave dalla finestra di dialogo visualizzata. Se il valore della parola chiave viene passato nella stringa di connessione e l'utente non modifica il valore per la parola chiave nella finestra di dialogo, il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client utilizza il valore dalla stringa di connessione. Se il valore non è impostato nella stringa di connessione e l'utente non esegue alcuna assegnazione nella finestra di dialogo, il driver utilizza il valore predefinito.  
  
 `SQLDriverConnect`è necessario specificare un *WindowHandle* valido quando un qualsiasi valore *DriverCompletion* richiede o potrebbe richiedere la visualizzazione della finestra di dialogo di connessione del driver. Un handle non valido restituisce SQL_ERROR.  
  
 Specificare la parola chiave DRIVER o DSN. ODBC dichiara che un driver utilizza la parola chiave più a sinistra tra le due e ignora l'altra se sono specificate entrambe. Se viene specificato il DRIVER oppure è l'oggetto più a sinistra dei due e il `SQLDriverConnect` valore del parametro *DriverCompletion* è SQL_DRIVER_NOPROMPT, la parola chiave server e un valore appropriato sono obbligatori.  
  
 Quando si specifica SQL_DRIVER_NOPROMPT, le parole chiave di autenticazione utente devono essere presenti con valori. Il driver garantisce la presenza della stringa "Trusted_Connection=yes" o delle parole chiave UID e PWD.  
  
 Se il valore del parametro *DriverCompletion* è SQL_DRIVER_NOPROMPT o SQL_DRIVER_COMPLETE_REQUIRED e la lingua o il database deriva dalla stringa di connessione e non è valido, `SQLDriverConnect` restituisce SQL_ERROR.  
  
 Se il valore del parametro *DriverCompletion* è SQL_DRIVER_NOPROMPT o SQL_DRIVER_COMPLETE_REQUIRED e la lingua o il database deriva dalle definizioni delle origini dati ODBC e non è valido, `SQLDriverConnect` utilizza la lingua o il database predefinito per l'ID utente specificato e restituisce SQL_SUCCESS_WITH_INFO.  
  
 Se il valore del parametro *DriverCompletion* è SQL_DRIVER_COMPLETE o SQL_DRIVER_PROMPT e se la lingua o il database non è valido, `SQLDriverConnect` Visualizza nuovamente la finestra di dialogo.  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>Supporto di SQLDriverConnect per il ripristino di emergenza a disponibilità elevata  
 Per ulteriori informazioni sull'utilizzo `SQLDriverConnect` di per la connessione a un [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] cluster, vedere [SQL Server Native client supporto per la disponibilità elevata e il ripristino di emergenza](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>Supporto di SQLDriverConnect per nomi SPN (Service Principal Name)  
 SQLDDriverConnect utilizzerà la finestra di dialogo di accesso ODBC boxwhen la richiesta di conferma è abilitata. Ciò consente di immettere i nomi SPN per il server principale e per il relativo partner di failover.  
  
 SQLDriverConnect accetterà le nuove parole chiave della stringa `ServerSPN` di connessione e `FailoverPartnerSPN` rileverà i nuovi attributi di connessione SQL_COPT_SS_SERVER_SPN e SQL_COPT_SS_FAILOVER_PARTNER_SPN.  
  
 Quando un attributo di connessione viene specificato più di una volta, un valore impostato a livello di programmazione ha la precedenza sul valore in un DSN e su un valore in una stringa di connessione. Un valore in un DSN ha la precedenza su un valore in una stringa di connessione.  
  
 Quando si apre una connessione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client imposta SQL_COPT_SS_MUTUALLY_AUTHENTICATED e SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD sul metodo di autenticazione utilizzato per aprire la connessione.  
  
 Per ulteriori informazioni sui nomi SPN, vedere [nomi dell'entità servizio &#40;spn&#41; nelle connessioni Client &#40;ODBC&#41;](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="examples"></a>Esempio  
 Nella chiamata seguente viene illustrata la quantità minima di dati necessaria per `SQLDriverConnect` :  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 Le stringhe di connessione seguenti illustrano i dati minimi necessari quando il valore del parametro *DriverCompletion* è SQL_DRIVER_NOPROMPT:  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SQLDriverConnect (funzione)](https://go.microsoft.com/fwlink/?LinkId=59340)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)   
 [IMPOSTA ANSI_NULLS &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [IMPOSTA ANSI_PADDING &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)  
  
  
