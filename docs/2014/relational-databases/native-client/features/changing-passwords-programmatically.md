---
title: Modifica delle password a livello di codice | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ec1db8e0f88bea5a02eb54b94a88194882ad9ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046253"
---
# <a name="changing-passwords-programmatically"></a>Modifica delle password a livello di programmazione
  Nelle versioni precedenti a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] una password di un utente scaduta può essere reimpostata solo da un amministratore. A partire [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta la gestione della scadenza della password a livello di codice sia tramite il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client e il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client e attraverso modifiche al **Account di accesso di SQL Server** finestre di dialogo.  
  
> [!NOTE]  
>  Quando possibile, richiedere agli utenti di immettere le credenziali in fase di esecuzione ed evitare di archiviarle in un formato persistente. Se è necessario rendere persistenti le credenziali, è consigliabile crittografarle usando l'[API di crittografia Win32](https://go.microsoft.com/fwlink/?LinkId=64532). Per altre informazioni sull'uso delle password, vedere [Password complesse](../../security/strong-passwords.md).  
  
## <a name="sql-server-login-error-codes"></a>Codici di errore degli account di accesso di SQL Server  
 Quando non è possibile stabilire una connessione a causa di problemi di autenticazione, sarà disponibile uno dei codici di errore di SQL Server seguenti per consentire la diagnosi e il recupero.  
  
|Codice di errore di SQL Server|Messaggio di errore|  
|---------------------------|-------------------|  
|15113|Accesso non riuscito per l'utente ' %. * motivo ls': Impossibile convalidare la password. L'account è bloccato.|  
|18463|Accesso non riuscito per l'utente '%.*ls'. Motivo: Modifica della password non è riuscita. Impossibile utilizzare la password in questo momento.|  
|18464|Accesso non riuscito per l'utente '%.*ls'. Motivo: Modifica della password non è riuscita. La password non soddisfa i criteri di Windows in quanto è troppo breve.|  
|18465|Accesso non riuscito per l'utente '%.*ls'. Motivo: Modifica della password non è riuscita. La password non soddisfa i criteri di Windows in quanto è troppo lunga.|  
|18466|Accesso non riuscito per l'utente '%.*ls'. Motivo: Modifica della password non è riuscita. La password non soddisfa i criteri di Windows in quanto non è sufficientemente complessa.|  
|18467|Accesso non riuscito per l'utente '%.*ls'. Motivo: Modifica della password non è riuscita. La password non soddisfa i requisiti della DLL per il filtro delle password.|  
|18468|Accesso non riuscito per l'utente '%.*ls'. Motivo: Modifica della password non è riuscita. Si è verificato un errore imprevisto durante la convalida della password.|  
|18487|Accesso non riuscito per l'utente '%.*ls'. Motivo: La password dell'account è scaduta.|  
|18488|Accesso non riuscito per l'utente '%.*ls'. Motivo: La password dell'account deve essere modificata.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provider OLE DB di SQL Server Native Client  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta la scadenza password mediante un'interfaccia utente e a livello di codice.  
  
### <a name="ole-db-user-interface-password-expiration"></a>Scadenza password dell'interfaccia utente OLE DB  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta la scadenza password mediante le modifiche apportate per il **account di accesso di SQL Server** finestre di dialogo. Se il valore di DBPROP_INIT_PROMPT è impostato su DBPROMPT_NOPROMPT, il tentativo di connessione iniziale non riesce se la password è scaduta.  
  
 Se DBPROP_INIT_PROMPT è stato impostato su qualsiasi altro valore, viene visualizzata la finestra di dialogo **Account di accesso di SQL Server** indipendentemente dalla scadenza della password. L'utente può cambiare la password facendo clic sul pulsante **Opzioni** e selezionando **Cambia password**.  
  
 Se l'utente fa clic su OK e la password è scaduta, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] richiede all'utente di immettere e confermare una nuova password usando la finestra di dialogo **Modifica password SQL Server**.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>Comportamento del prompt di OLE DB e account bloccati  
 È possibile che non si riesca a stabilire una connessione perché l'account è bloccato. Se questo problema si verifica in seguito alla visualizzazione della finestra di dialogo **Account di accesso di SQL Server**, viene visualizzato il messaggio di errore del server e il tentativo di connessione viene interrotto. Il problema può verificarsi anche se, in seguito alla visualizzazione della finestra di dialogo **Modifica password SQL Server**, l'utente immette un valore non corretto per la vecchia password. In questo caso viene visualizzato lo stesso messaggio di errore e il tentativo di connessione viene interrotto.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>Pool di connessioni OLE DB, scadenza password e account bloccati  
 Un account può essere bloccato o la rispettiva password può scadere mentre la connessione è ancora attiva in un pool di connessioni. Il server controlla le password scadute e gli account bloccati in due circostanze. Quando una connessione viene creata per la prima volta e quando la connessione viene reimpostata, ovvero quando viene estratta dal pool.  
  
 Quando il tentativo di ripristino non riesce, la connessione viene rimossa dal pool e viene restituito un errore.  
  
### <a name="ole-db-programmatic-password-expiration"></a>Scadenza password OLE DB a livello di programmazione  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta la scadenza password mediante l'aggiunta della proprietà SSPROP_AUTH_OLD_PASSWORD (tipo VT_BSTR) che è stato aggiunto al set di proprietà DBPROPSET_SQLSERVERDBINIT.  
  
 La proprietà "Password" esistente si riferisce a DBPROP_AUTH_PASSWORD e viene utilizzata per archiviare la nuova password.  
  
> [!NOTE]  
>  Nella stringa di connessione la proprietà "Vecchia password" imposta SSPROP_AUTH_OLD_PASSWORD, ovvero la password corrente (probabilmente scaduta) che non è disponibile tramite una proprietà della stringa del provider.  
  
 Il provider non rende persistente il valore di questa proprietà. Quando questa proprietà è impostata, il provider non utilizza il pool di connessioni per la prima connessione, dal momento che verrà stabilita una nuova connessione. Dopo aver cambiato la password, non sarà più possibile utilizzare la connessione corrente in quanto contiene ancora la vecchia password che non è più valida. Se inoltre si riesce ad accedere, il provider cancella questa proprietà. I tentativi successivi di recuperare la vecchia password restituiscono VT_EMPTY.  
  
> [!NOTE]  
>  SSPROP_AUTH_OLD_PASSWORD non deve essere resa persistente in quanto viene utilizzata solo quando una password è scaduta.  
  
 Ogni volta che la proprietà "Vecchia password" viene impostata, il provider presuppone che sia in atto un tentativo di modificare la password, a meno che non venga specificata anche l'autenticazione di Windows. In questo caso, questa avrebbe comunque ha la precedenza.  
  
 Se si usa l'autenticazione di Windows, l'immissione della vecchia password restituisce DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED, a seconda se la vecchia password è stata specificata rispettivamente come REQUIRED o OPTIONAL e il valore dello stato di DBPROPSTATUS_CONFLICTINGBADVALUE viene restituito in *dwStatus*. Questo errore viene rilevato quando viene chiamato **IDBInitialize::Initialize**.  
  
 Se un tentativo di modificare la password non riesce in modo imprevisto, il server restituisce il codice di errore 18468. Dal tentativo di connessione viene restituito un errore OLE DB standard.  
  
 Per altre informazioni sul set di proprietà DBPROPSET_SQLSERVERDBINIT, vedere [proprietà di inizializzazione e autorizzazione](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC di SQL Server Native Client  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta la scadenza password mediante un'interfaccia utente e a livello di codice.  
  
### <a name="odbc-user-interface-password-expiration"></a>Scadenza password dell'interfaccia utente ODBC  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta la scadenza password mediante le modifiche apportate per il **account di accesso di SQL Server** finestre di dialogo.  
  
 Se [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md) viene chiamato e il valore di **DriverCompletion** è impostato su SQL_DRIVER_NOPROMPT, il tentativo di connessione iniziale non riesce se la password è scaduta. Il valore SQLSTATE 28000 e il valore 18487 del codice di errore nativo vengono restituiti dalle chiamate successive a **SQLError** oppure **SQLGetDiagRec**.  
  
 Se **DriverCompletion** è stato impostato su qualsiasi altro valore, l'utente vede il **account di accesso di SQL Server** finestra di dialogo, indipendentemente dal fatto o meno la password è scaduta. L'utente può cambiare la password facendo clic sul pulsante **Opzioni** e selezionando **Cambia password**.  
  
 Se l'utente fa clic su OK e la password è scaduta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] istruzioni per immettere e confermare una nuova password utilizzando la **modifica Password SQL Server** finestra di dialogo.  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>Comportamento del prompt di ODBC e account bloccati  
 È possibile che non si riesca a stabilire una connessione perché l'account è bloccato. Se questo problema si verifica in seguito alla visualizzazione della finestra di dialogo **Account di accesso di SQL Server**, viene visualizzato il messaggio di errore del server e il tentativo di connessione viene interrotto. Il problema può verificarsi anche se, in seguito alla visualizzazione della finestra di dialogo **Modifica password SQL Server**, l'utente immette un valore non corretto per la vecchia password. In questo caso viene visualizzato lo stesso messaggio di errore e il tentativo di connessione viene interrotto.  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>Pool di connessioni ODBC, scadenza password e account bloccati  
 Un account può essere bloccato o la rispettiva password può scadere mentre la connessione è ancora attiva in un pool di connessioni. Il server controlla le password scadute e gli account bloccati in due circostanze. Quando una connessione viene creata per la prima volta e quando la connessione viene reimpostata, ovvero quando viene estratta dal pool.  
  
 Quando il tentativo di ripristino non riesce, la connessione viene rimossa dal pool e viene restituito un errore.  
  
### <a name="odbc-programmatic-password-expiration"></a>Scadenza password ODBC a livello di programmazione  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta la scadenza password mediante l'aggiunta dell'attributo SQL_COPT_SS_OLDPWD che è impostato prima della connessione al server usando il [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) (funzione).  
  
 L'attributo SQL_COPT_SS_OLDPWD dell'handle di connessione si riferisce alla password scaduta. Per questo attributo non è disponibile un attributo di stringa di connessione, in quanto interferirebbe con il pool di connessioni. Se si riesce ad accedere, il driver cancella questo attributo.  
  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client restituisce SQL_ERROR in quattro casi per questa caratteristica: scadenza della password, conflitto dei criteri password, blocco dell'account e quando è impostata la proprietà della vecchia password quando si usa l'autenticazione di Windows. Il driver restituisce all'utente i messaggi di errore appropriati quando [SQLGetDiagField](../../native-client-odbc-api/sqlgetdiagfield.md) viene richiamato.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](sql-server-native-client-features.md)  
  
  
