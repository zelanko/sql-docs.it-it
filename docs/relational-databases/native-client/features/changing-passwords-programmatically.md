---
description: Modifica SQL Server Native Client password a livello di codice
title: Modifica delle password a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], password expiration
- SQL Server Native Client ODBC driver, passwords
- SQL Server Native Client OLE DB provider, passwords
- passwords [SQL Server], expiration
- SQLNCLI, password expiration
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- expired passwords [SQL Server Native Client]
- SQL Server Native Client, password expiration
- modifying passwords
ms.assetid: 624ad949-5fed-4ce5-b319-878549f9487b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a356ea0603d096fc339495f028b1e4f86af81f92
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463382"
---
# <a name="changing-sql-server-native-client-passwords-programmatically"></a>Modifica SQL Server Native Client password a livello di codice
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Nelle versioni precedenti a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] una password di un utente scaduta può essere reimpostata solo da un amministratore. A partire da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] , [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta la gestione della scadenza delle password a livello di programmazione tramite il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native client e il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native client e le modifiche apportate alle finestre di dialogo **SQL Server account di accesso** .  
  
> [!NOTE]  
>  Quando possibile, richiedere agli utenti di immettere le credenziali in fase di esecuzione ed evitare di archiviarle in un formato persistente. Se è necessario rendere persistenti le credenziali, è consigliabile crittografarle usando l'[API di crittografia Win32](/windows/win32/seccrypto/cryptography-reference). Per altre informazioni sull'uso delle password, vedere [Password complesse](../../../relational-databases/security/strong-passwords.md).  
  
## <a name="sql-server-login-error-codes"></a>Codici di errore degli account di accesso di SQL Server  
 Quando non è possibile stabilire una connessione a causa di problemi di autenticazione, sarà disponibile uno dei codici di errore di SQL Server seguenti per consentire la diagnosi e il recupero.  
  
|Codice di errore di SQL Server|Messaggio di errore|  
|---------------------------|-------------------|  
|15113|Accesso non riuscito per l'utente '%.*ls' Motivo: impossibile convalidare la password. L'account è bloccato.|  
|18463|Accesso non riuscito per l'utente '%.*ls'. Motivo: impossibile modificare la password. Impossibile utilizzare la password in questo momento.|  
|18464|Accesso non riuscito per l'utente '%.*ls'. Motivo: impossibile modificare la password. La password non soddisfa i criteri di Windows in quanto è troppo breve.|  
|18465|Accesso non riuscito per l'utente '%.*ls'. Motivo: impossibile modificare la password. La password non soddisfa i criteri di Windows in quanto è troppo lunga.|  
|18466|Accesso non riuscito per l'utente '%.*ls'. Motivo: impossibile modificare la password. La password non soddisfa i criteri di Windows in quanto non è sufficientemente complessa.|  
|18467|Accesso non riuscito per l'utente '%.*ls'. Motivo: impossibile modificare la password. La password non soddisfa i requisiti della DLL per il filtro delle password.|  
|18468|Accesso non riuscito per l'utente '%.*ls'. Motivo: impossibile modificare la password. Si è verificato un errore imprevisto durante la convalida della password.|  
|18487|Accesso non riuscito per l'utente '%.*ls'. Motivo: la password dell'account è scaduta.|  
|18488|Accesso non riuscito per l'utente '%.*ls'. Motivo: è necessario modificare la password dell'account.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provider OLE DB di SQL Server Native Client  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client supporta la scadenza delle password tramite un'interfaccia utente e a livello di codice.  
  
### <a name="ole-db-user-interface-password-expiration"></a>Scadenza password dell'interfaccia utente OLE DB  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client supporta la scadenza delle password tramite le modifiche apportate alle finestre di dialogo **SQL Server account di accesso** . Se il valore di DBPROP_INIT_PROMPT è impostato su DBPROMPT_NOPROMPT, il tentativo di connessione iniziale non riesce se la password è scaduta.  
  
 Se DBPROP_INIT_PROMPT è stato impostato su qualsiasi altro valore, viene visualizzata la finestra di dialogo **Account di accesso di SQL Server** indipendentemente dalla scadenza della password. L'utente può cambiare la password facendo clic sul pulsante **Opzioni** e selezionando **Cambia password**.  
  
 Se l'utente fa clic su OK e la password è scaduta, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] richiede all'utente di immettere e confermare una nuova password usando la finestra di dialogo **Modifica password SQL Server**.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>Comportamento del prompt di OLE DB e account bloccati  
 È possibile che non si riesca a stabilire una connessione perché l'account è bloccato. Se questo problema si verifica in seguito alla visualizzazione della finestra di dialogo **Account di accesso di SQL Server**, viene visualizzato il messaggio di errore del server e il tentativo di connessione viene interrotto. Il problema può verificarsi anche se, in seguito alla visualizzazione della finestra di dialogo **Modifica password SQL Server**, l'utente immette un valore non corretto per la vecchia password. In questo caso viene visualizzato lo stesso messaggio di errore e il tentativo di connessione viene interrotto.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>Pool di connessioni OLE DB, scadenza password e account bloccati  
 Un account può essere bloccato o la rispettiva password può scadere mentre la connessione è ancora attiva in un pool di connessioni. Il server controlla le password scadute e gli account bloccati in due circostanze. Quando una connessione viene creata per la prima volta e quando la connessione viene reimpostata, ovvero quando viene estratta dal pool.  
  
 Quando il tentativo di ripristino non riesce, la connessione viene rimossa dal pool e viene restituito un errore.  
  
### <a name="ole-db-programmatic-password-expiration"></a>Scadenza password OLE DB a livello di programmazione  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client supporta la scadenza delle password tramite l'aggiunta della proprietà SSPROP_AUTH_OLD_PASSWORD (type VT_BSTR) aggiunta al set di proprietà DBPROPSET_SQLSERVERDBINIT.  
  
 La proprietà "Password" esistente si riferisce a DBPROP_AUTH_PASSWORD e viene utilizzata per archiviare la nuova password.  
  
> [!NOTE]  
>  Nella stringa di connessione la proprietà "Vecchia password" imposta SSPROP_AUTH_OLD_PASSWORD, ovvero la password corrente (probabilmente scaduta) che non è disponibile tramite una proprietà della stringa del provider.  
  
 Il provider non rende persistente il valore di questa proprietà. Quando questa proprietà è impostata, il provider non utilizza il pool di connessioni per la prima connessione, dal momento che verrà stabilita una nuova connessione. Dopo aver cambiato la password, non sarà più possibile utilizzare la connessione corrente in quanto contiene ancora la vecchia password che non è più valida. Se inoltre si riesce ad accedere, il provider cancella questa proprietà. I tentativi successivi di recuperare la vecchia password restituiscono VT_EMPTY.  
  
> [!NOTE]  
>  SSPROP_AUTH_OLD_PASSWORD non deve essere resa persistente in quanto viene utilizzata solo quando una password è scaduta.  
  
 Ogni volta che la proprietà "Vecchia password" viene impostata, il provider presuppone che sia in atto un tentativo di modificare la password, a meno che non venga specificata anche l'autenticazione di Windows. In questo caso, questa avrebbe comunque ha la precedenza.  
  
 Se si usa l'autenticazione di Windows, l'immissione della vecchia password restituisce DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED, a seconda se la vecchia password è stata specificata rispettivamente come REQUIRED o OPTIONAL e il valore dello stato di DBPROPSTATUS_CONFLICTINGBADVALUE viene restituito in *dwStatus*. Questo errore viene rilevato quando viene chiamato **IDBInitialize::Initialize**.  
  
 Se un tentativo di modificare la password non riesce in modo imprevisto, il server restituisce il codice di errore 18468. Dal tentativo di connessione viene restituito un errore OLE DB standard.  
  
 Per altre informazioni sul set di proprietà DBPROPSET_SQLSERVERDBINIT, vedere [Proprietà di inizializzazione e di autorizzazione](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC di SQL Server Native Client  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client supporta la scadenza delle password tramite un'interfaccia utente e a livello di codice.  
  
### <a name="odbc-user-interface-password-expiration"></a>Scadenza password dell'interfaccia utente ODBC  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta la scadenza delle password tramite le modifiche apportate alle finestre di dialogo di **accesso SQL Server** .  
  
 Se viene chiamato [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) e il valore di **DriverCompletion** è impostato su SQL_DRIVER_NOPROMPT, il tentativo di connessione iniziale non riesce se la password è scaduta. Il valore SQLSTATE 28000 e il valore del codice di errore nativo 18487 vengono restituiti dalle chiamate successive a **SQLError** o **SQLGetDiagRec**.  
  
 Se **DriverCompletion** è stato impostato su qualsiasi altro valore, l'utente Visualizza la finestra di dialogo **SQL Server login** , indipendentemente dal fatto che la password sia scaduta o meno. L'utente può cambiare la password facendo clic sul pulsante **Opzioni** e selezionando **Cambia password**.  
  
 Se l'utente fa clic su OK e la password è scaduta, viene [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] richiesto di immettere e confermare una nuova password utilizzando la finestra di dialogo **Cambia SQL Server password** .  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>Comportamento del prompt di ODBC e account bloccati  
 È possibile che non si riesca a stabilire una connessione perché l'account è bloccato. Se questo problema si verifica in seguito alla visualizzazione della finestra di dialogo **Account di accesso di SQL Server**, viene visualizzato il messaggio di errore del server e il tentativo di connessione viene interrotto. Il problema può verificarsi anche se, in seguito alla visualizzazione della finestra di dialogo **Modifica password SQL Server**, l'utente immette un valore non corretto per la vecchia password. In questo caso viene visualizzato lo stesso messaggio di errore e il tentativo di connessione viene interrotto.  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>Pool di connessioni ODBC, scadenza password e account bloccati  
 Un account può essere bloccato o la rispettiva password può scadere mentre la connessione è ancora attiva in un pool di connessioni. Il server controlla le password scadute e gli account bloccati in due circostanze. Quando una connessione viene creata per la prima volta e quando la connessione viene reimpostata, ovvero quando viene estratta dal pool.  
  
 Quando il tentativo di ripristino non riesce, la connessione viene rimossa dal pool e viene restituito un errore.  
  
### <a name="odbc-programmatic-password-expiration"></a>Scadenza password ODBC a livello di programmazione  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta la scadenza delle password mediante l'aggiunta dell'attributo SQL_COPT_SS_OLDPWD impostato prima della connessione al server tramite la funzione [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) .  
  
 L'attributo SQL_COPT_SS_OLDPWD dell'handle di connessione si riferisce alla password scaduta. Per questo attributo non è disponibile un attributo di stringa di connessione, in quanto interferirebbe con il pool di connessioni. Se si riesce ad accedere, il driver cancella questo attributo.  
  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client restituisce SQL_ERROR in quattro casi per questa funzionalità: scadenza password, conflitto tra criteri password, blocco account e quando la proprietà vecchia password viene impostata durante l'utilizzo dell'autenticazione di Windows. Il driver restituisce all'utente i messaggi di errore appropriati quando viene richiamato [SQLGetDiagField](../../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
