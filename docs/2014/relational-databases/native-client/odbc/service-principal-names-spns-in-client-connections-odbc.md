---
title: Nomi delle entità servizio (SPN) nelle connessioni Client (ODBC) | Documenti di Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 1d60cb30-4c46-49b2-89ab-701e77a330a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f45e6124dbbad79802e290f935ccc6f3f45cee0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63144404"
---
# <a name="service-principal-names-spns-in-client-connections-odbc"></a>Nomi SPN (Service Principal Name) nelle connessioni client (ODBC)
  In questo argomento vengono descritti gli attributi e le funzioni ODBC che supportano i nomi SPN (Service Principal Name, nome dell'entità servizio) nelle applicazioni client. Per ulteriori informazioni su SPN nelle applicazioni client, vedere [nome principale servizio &#40;SPN&#41; il supporto di connessioni Client](../features/service-principal-name-spn-support-in-client-connections.md) e [ottenere l'autenticazione reciproca Kerberos](../../native-client-odbc-how-to/get-mutual-kerberos-authentication.md).  
  
## <a name="connection-string-keywords"></a>Parole chiave per le stringhe di connessione  
 Le parole chiave per le stringhe di connessione seguenti consentono la specifica di un nome SPN nelle applicazioni client.  
  
|Parola chiave|Value|  
|-------------|-----------|  
|`ServerSPN`|Nome SPN del server. Il valore predefinito è una stringa vuota. In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client tale stringa causa l'utilizzo del nome SPN predefinito generato dal driver.|  
|`FailoverPartnerSPN`|Nome SPN del partner di failover. Il valore predefinito è una stringa vuota. In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client tale stringa causa l'utilizzo del nome SPN predefinito generato dal driver.|  
  
## <a name="connection-attributes"></a>Attributi di connessione  
 Gli attributi di connessione seguenti consentono la specifica di un nome SPN e di una query per il metodo di autenticazione nelle applicazioni client.  
  
|Nome|Type|Uso|  
|----------|----------|-----------|  
|SQL_COPT_SS_SERVER_SPN<br /><br /> SQL_COPT_SS_FAILOVER_PARTNER_SPN|SQLTCHAR, lettura/scrittura|Specifica il nome SPN per il server. Il valore predefinito è una stringa vuota. In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client tale stringa causa l'utilizzo del nome SPN predefinito generato dal driver.<br /><br /> Su questo attributo è possibile eseguire una query solo in seguito alla relativa impostazione a livello di codice o all'apertura di una connessione. Se si tenta di eseguire una query su questo attributo in una connessione non aperta e con l'attributo non impostato a livello di codice, viene restituito SQL_ERROR e viene registrato un record di diagnostica con SQLState 08003 e il messaggio "Connessione non aperta".<br /><br /> Se si tenta di impostare l'attributo quando una connessione è aperta, viene restituito SQL_ERROR e viene registrato un record di diagnostica con SQLState HY011 e il messaggio "Operazione correntemente non valida".|  
|SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD|SQLTCHAR, sola lettura|Restituisce il metodo di autenticazione utilizzato per la connessione. Il valore restituito all'applicazione è il valore che Windows restituisce a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. I valori possibili sono:<br /><br /> -"NTLM", viene restituito quando viene aperta una connessione utilizzando l'autenticazione NTLM.<br />-"Kerberos", viene restituito quando viene aperta una connessione mediante l'autenticazione Kerberos.<br /><br /> Questo attributo può essere letto solo per una connessione aperta in cui è stata utilizzata l'autenticazione di Windows. Se si tenta di leggerlo prima che venga aperta una connessione, viene restituito SQL_ERROR e viene registrato un errore con SQLState 08003 e il messaggio "Connessione non aperta".<br /><br /> Se si esegue una query su questo attributo in una connessione in cui non è stata utilizzata l'autenticazione di Windows, viene restituito SQL_ERROR e viene registrato un errore con SQLState HY092 e il messaggio "Identificatore di opzione o di attributo non valido (SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD è disponibile solo per connessioni trusted)".<br /><br /> Se non è possibile determinare il metodo di autenticazione, viene restituito SQL_ERROR e viene registrato un errore con SQLState HY000 e il messaggio "Errore generale".|  
|SQL_COPT_SS_MUTUALLY_AUTHENTICATED|SQLSMALLINT, sola lettura|Restituisce SQL_TRUE se nella connessione è stata eseguita un'autenticazione reciproca del server. In caso contrario, restituisce SQL_FALSE.<br /><br /> Questo attributo può essere letto solo per una connessione aperta. Se si tenta di leggerlo prima che venga aperta una connessione, viene restituito SQL_ERROR e viene registrato un errore con SQLState 08003 e il messaggio "Connessione non aperta".<br /><br /> Se viene eseguita una query sull'attributo per una connessione in cui non è stata utilizzata l'autenticazione di Windows, viene restituito SQL_FALSE.|  
  
## <a name="odbc-function-support-for-specifying-spns"></a>Supporto delle funzioni ODBC per la specifica dei nomi SPN  
 Le funzioni ODBC seguenti supportano le applicazioni client e i nomi SPN:  
  
-   [SQLBrowseConnect](../../native-client-odbc-api/sqlbrowseconnect.md)  
  
-   [SQLConnect](../../native-client-odbc-api/sqlconnect.md)  
  
-   [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md)  
  
-   [SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md)  
  
-   [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
