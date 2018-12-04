---
title: Tramite Azure Active Directory con il Driver ODBC | Documentazione di Microsoft per SQL Server
ms.custom: ''
ms.date: 11/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7273baec814905d86e431c5a6a8f13313b9743e4
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52536655"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Uso di Azure Active Directory con il driver ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>Scopo

Microsoft ODBC Driver for SQL Server con la versione 13.1 o successiva consente alle applicazioni di ODBC per connettersi a un'istanza di SQL Azure usando un'identità federata in Azure Active Directory con un nome utente/password, un token di accesso di Azure Active Directory o Windows L'autenticazione integrata (_solo i driver di Windows_). Per il Driver ODBC versione 13.1, l'accesso di Azure Active Directory è l'autenticazione tramite token _solo Windows_. Il Driver ODBC versione 17 e versioni successive supportano questa autenticazione tutte le piattaforme (Windows, Linux e Mac). Una nuova autenticazione interattiva di Azure Active Directory con l'ID di accesso è stato introdotto nel Driver ODBC versione 17.1 per Windows. Tutti questi componenti vengono eseguiti tramite l'uso di nuovo DSN e parole chiave delle stringhe di connessione e gli attributi di connessione.

> [!NOTE]
> Il Driver ODBC in Linux e macOS non supporta Active Directory Federation Services. Se si utilizza l'autenticazione di nome utente e password di Azure Active Directory da un Linux o macOS client e la configurazione di Active Directory include servizi federati, l'autenticazione potrebbe non riuscire.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>DSN nuovi e/o modificati e parole chiave delle stringhe di connessione

Il `Authentication` parola chiave può essere utilizzata quando ci si connette con una stringa di connessione o DSN per controllare la modalità di autenticazione. Il valore impostato nella stringa di connessione sostituisce quella nel DSN, se specificato. Il _pre-valore dell'attributo_ del `Authentication` impostazione è il valore calcolato dai valori DSN e stringa di connessione.

|nome|Valori|Default|Descrizione|
|-|-|-|-|
|`Authentication`|(non impostato), (stringa vuota), `SqlPassword`, `ActiveDirectoryPassword`, `ActiveDirectoryIntegrated`, `ActiveDirectoryInteractive`|(non impostato)|Controlla la modalità di autenticazione.<table><tr><th>valore<th>Descrizione<tr><td>(non impostato)<td>Modalità di autenticazione di base a parole chiave (opzioni di connessione legacy esistenti).<tr><td>(stringa vuota)<td>Stringa di connessione: "{0}" Eseguire l'override e annullare un `Authentication` impostata nel DSN.<tr><td>`SqlPassword`<td>L'autenticazione diretta a un'istanza di SQL Server utilizzando un nome utente e password.<tr><td>`ActiveDirectoryPassword`<td>Eseguire l'autenticazione con un'identità di Azure Active Directory usando un nome utente e password.<tr><td>`ActiveDirectoryIntegrated`<td>_Solo i driver di Windows_. Eseguire l'autenticazione con un'identità di Azure Active Directory usando l'autenticazione integrata.<tr><td>`ActiveDirectoryInteractive`<td>_Solo i driver di Windows_. Eseguire l'autenticazione con un'identità di Azure Active Directory usando l'autenticazione interattiva.</table>|
|`Encrypt`|(non impostato), `Yes`, `No`|(vedere la descrizione)|Controlla la crittografia per una connessione. Se il valore pre-dell'attributo di i `Authentication` impostazione non è _none_ nella stringa di connessione o DSN, il valore predefinito è `Yes`. Diversamente, il valore predefinito è `No`. Se l'attributo `SQL_COPT_SS_AUTHENTICATION` sostituisce il valore pre-dell'attributo di `Authentication`, in modo esplicito impostare il valore della crittografia nelle attributo di connessione o DSN o stringa di connessione. È il valore dell'attributo non definitiva di crittografia `Yes` se il valore è impostato su `Yes` nella stringa di connessione o DSN.|

## <a name="new-andor-modified-connection-attributes"></a>Attributi di connessione nuovi e/o modificato

Di seguito pre-connessione connessione gli attributi sono stati introdotti o modificati per supportare l'autenticazione di Azure Active Directory. Quando un attributo di connessione dispone di una stringa di connessione corrispondente o una parola chiave DSN e viene impostato, l'attributo di connessione ha la precedenza.

|attribute|Tipo|Valori|Default|Descrizione|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_RESET`|(non impostato)|Vedere la descrizione di `Authentication` parola chiave precedente. `SQL_AU_NONE` viene fornito per eseguire l'override esplicito di un set `Authentication` valore nella stringa DSN e/o di connessione, mentre `SQL_AU_RESET` deseleziona l'attributo se è stata impostata, consentendo il valore di stringa di connessione o DSN hanno la precedenza.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|Puntatore a `ACCESSTOKEN` o NULL|NULL|Se diverso da null, specifica di Token di accesso di Azure ad da usare. È possibile specificare un token di accesso, nonché `UID`, `PWD`, `Trusted_Connection`, o `Authentication` parole chiave delle stringhe di connessione o i relativi attributi equivalente. <br> **Nota:** Driver ODBC versione 13.1 questo supporta solo sugli _Windows_.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(vedere la descrizione)|Controlla la crittografia per una connessione. `SQL_EN_OFF` e `SQL_EN_ON` disabilitare e abilitare la crittografia, rispettivamente. Se il valore pre-dell'attributo di il `Authentication` impostazione non è _none_ oppure `SQL_COPT_SS_ACCESS_TOKEN` è impostato, e `Encrypt` non è stato specificato nella stringa di connessione o DSN, il valore predefinito è `SQL_EN_ON`. Diversamente, il valore predefinito è `SQL_EN_OFF`. Se l'attributo di connessione `SQL_COPT_SS_AUTHENTICATION` è impostato su non _none_, impostare in modo esplicito `SQL_COPT_SS_ENCRYPT` sul valore desiderato se `Encrypt` non è stato specificato nella stringa di connessione o DSN. Il valore effettivo dei controlli attributo [se la crittografia verrà utilizzata per la connessione.](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|Non è supportata con Azure Active Directory, poiché le modifiche delle password per le identità di AAD non può essere eseguite tramite una connessione ODBC. <br><br>In SQL Server 2005 è stata introdotta la scadenza della password per l'autenticazione di SQL Server. Il `SQL_COPT_SS_OLDPWD` attributo è stato aggiunto per consentire al client di fornire sia la vecchia che la nuova password per la connessione. Quando questa proprietà è impostata, il provider non utilizzerà il pool di connessioni per la prima connessione o per le connessioni successive, in quanto la stringa di connessione conterrà la password precedente che è stata modificata.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_Deprecata_; usare `SQL_COPT_SS_AUTHENTICATION` impostato su `SQL_AU_AD_INTEGRATED` invece. <br><br>Forza utilizza dell'autenticazione di Windows (Kerberos in Linux e macOS) per la convalida di accesso sull'accesso al server. Quando viene utilizzata l'autenticazione di Windows, il driver ignora i valori di identificatore e la password utente forniti come parte della `SQLConnect`, `SQLDriverConnect`, o `SQLBrowseConnect` l'elaborazione.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Componenti aggiuntivi dell'interfaccia utente di Azure Active Directory (solo driver di Windows)

La configurazione del DSN e la connessione delle interfacce utente del driver sono stati migliorati con le opzioni aggiuntive necessarie per utilizzare l'autenticazione con Azure AD.

### <a name="creating-and-editing-dsns-in-the-ui"></a>Creazione e modifica dei DSN nell'interfaccia utente

È possibile usare il nuovo Azure AD le opzioni di autenticazione durante la creazione o la modifica di un DSN esistente usando l'interfaccia utente di installazione del driver:

`Authentication=ActiveDirectoryIntegrated` per l'autenticazione integrata di Azure Active Directory in SQL Azure

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword` per l'autenticazione di nome utente/password di Azure Active Directory in SQL Azure

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` per l'autenticazione interattiva di Azure Active Directory in SQL Azure

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword` per l'autenticazione di nome utente/password in SQL Server (Azure o in caso contrario)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes` per Windows autenticazione integrata di SSPI legacy

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

Le cinque opzioni corrispondono alle `Trusted_Connection=Yes` (Windows legacy esistenti SSPI sola l'autenticazione integrata) e `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword`, `ActiveDirectoryPassword`, e `ActiveDirectoryInteractive`, rispettivamente.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect prompt dei comandi (solo driver di Windows)

La finestra di dialogo dei messaggi di richiesta visualizzato dal SQLDriverConnect quando richiede le informazioni necessarie per completare la connessione contiene tre nuove opzioni per l'autenticazione di Azure AD:

![ServerLogin.png](windows/ServerLogin.png)

Queste opzioni corrispondono alle stesse cinque disponibile nella configurazione del DSN dell'interfaccia utente precedente.

### <a name="example-connection-strings"></a>Esempi di stringhe di connessione
1. Autenticazione di SQL Server - sintassi legacy. Certificato server non viene convalidato e viene utilizzata la crittografia solo se il server lo impone. Il nome utente e la password viene passata nella stringa di connessione.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. Autenticazione di SQL - nuova sintassi. Il client richiede la crittografia (il valore predefinito `Encrypt` viene `true`) e il certificato del server ottiene convalidato, indipendentemente dall'impostazione di crittografia (a meno che non `TrustServerCertificate` è impostata su `true`). Il nome utente e la password viene passata nella stringa di connessione.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. L'autenticazione di Windows (Kerberos in Linux e macOS) integrata tramite SSPI (per SQL Server o IaaS di SQL) - sintassi corrente. Certificato server non viene convalidato, a meno che non viene utilizzata la crittografia. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Solo i driver di Windows_.) L'autenticazione Windows integrata tramite SSPI (se il database di destinazione è in SQL Server o IaaS di SQL) - nuova sintassi. Il client richiede la crittografia (il valore predefinito `Encrypt` viene `true`) e il certificato del server ottiene convalidato, indipendentemente dall'impostazione di crittografia (a meno che non `TrustServerCertificate` è impostata su `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. Autenticazione di nome utente e Password di AAD (se il database di destinazione nel database SQL di Azure). Ottiene convalidare certificato del server, indipendentemente dall'impostazione di crittografia (a meno che `TrustServerCertificate` è impostata su `true`). Il nome utente e la password viene passata nella stringa di connessione. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Solo i driver di Windows_.) Autenticazione integrata di Windows con ADAL, che implica riscattare le credenziali dell'account di Windows per un token di accesso emesso da AAD, supponendo che il database di destinazione sia nel Database SQL di Azure. Ottiene convalidare certificato del server, indipendentemente dall'impostazione di crittografia (a meno che `TrustServerCertificate` è impostata su `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Solo i driver di Windows_.) Autenticazione interattiva di AAD viene utilizzata la tecnologia Azure multi-factor Authentication per impostare connessione. In questa modalità, fornendo l'ID di accesso, una finestra di dialogo di autenticazione di Windows Azure viene attivata e consente all'utente di immettere la password per completare la connessione. Il nome utente viene passato nella stringa di connessione.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

> [!NOTE] 
>- Quando si usano le nuove opzioni di Active Directory con il driver ODBC di Windows, assicurarsi che il [Active Directory Authentication Library per SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) sia stato installato. Quando si usa il driver di Linux e macOS, assicurarsi che `libcurl` è stato installato. Per la versione del driver 17.2 e versioni successive, questo non è una dipendenza esplicita poiché non è necessaria per altri metodi di autenticazione o operazioni di ODBC.
>- Per connettersi usando un nome utente dell'account SQL Server e una password, è possibile usare il nuovo `SqlPassword` opzione, è consigliata soprattutto per SQL Azure poiché questa opzione Abilita più sicuro le impostazioni predefinite di connessione.
>- Per connettersi usando un nome utente dell'account Azure Active Directory e una password, specificare `Authentication=ActiveDirectoryPassword` nella stringa di connessione e il `UID` e `PWD` parole chiave con il nome utente e password, rispettivamente.
>- Per connettersi usando l'autenticazione integrata di Active Directory (solo driver di Windows) o integrata di Windows, specificare `Authentication=ActiveDirectoryIntegrated` nella stringa di connessione. Il driver sceglierà automaticamente la modalità di autenticazione corretto. `UID` e `PWD` non deve essere specificata.
>- Per connettersi usando l'autenticazione di Active Directory Interactive (solo driver di Windows), `UID` deve essere specificato.

## <a name="authenticating-with-an-access-token"></a>L'autenticazione con un Token di accesso

Il `SQL_COPT_SS_ACCESS_TOKEN` attributo pre-connessione consente di usare un token di accesso ottenuto da Azure AD per l'autenticazione anziché nome utente e password, poiché elude inoltre la negoziazione e ottenere un token di accesso dal driver. Per usare un token di accesso, impostare il `SQL_COPT_SS_ACCESS_TOKEN` attributo di connessione a un puntatore a un `ACCESSTOKEN` struttura:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

Il `ACCESSTOKEN` è una struttura a lunghezza variabile costituita da 4 byte _lunghezza_ seguita da _lunghezza_ byte di dati opachi che formano il token di accesso. A causa di un modo in cui SQL Server gestisce i token di accesso, uno ottenuta tramite un [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) risposta JSON deve essere espanso in modo che ogni byte è seguito da 0 byte, simili a una stringa UCS-2 contenente solo caratteri ASCII di riempimento; tuttavia, il token è un valore opaco e la lunghezza specificata, in byte, non devono includere qualsiasi carattere di terminazione null. A causa di vincoli relativi notevole lunghezza e il formato, questo metodo di autenticazione è disponibile solo a livello di programmazione tramite le `SQL_COPT_SS_ACCESS_TOKEN` attributo di connessione; non sono parole chiave di stringa di connessione o DSN corrispondente. La stringa di connessione non deve contenere `UID`, `PWD`, `Authentication`, o `Trusted_Connection` parole chiave.

> [!NOTE]
> Il Driver ODBC versione 13.1 supporta solo l'autenticazione sul _Windows_.

## <a name="azure-active-directory-authentication-sample-code"></a>Codice di esempio dell'autenticazione di Azure Active Directory

L'esempio seguente viene illustrato il codice necessario per connettersi a SQL Server usando Azure Active Directory con parole chiave della connessione. Si noti che non è necessario modificare il codice dell'applicazione stessa. la stringa di connessione o DSN se viene utilizzato uno, è l'unica modifica necessaria per usare Azure Active Directory per l'autenticazione:
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
L'esempio seguente viene illustrato il codice necessario per connettersi a SQL Server usando Azure Active Directory con l'autenticazione di token di accesso. In questo caso, è necessario modificare il codice dell'applicazione per elaborare il token di accesso e impostare l'attributo di connessione associata.
~~~
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server}"
    SQLCHAR accessToken[] = "eyJ0eXAiOi..."; // In the format extracted from an OAuth JSON response
    ...
    DWORD dataSize = 2 * strlen(accessToken);
    ACCESSTOKEN *pAccToken = malloc(sizeof(ACCESSTOKEN) + dataSize);
    pAccToken->dataSize = dataSize;
    // Expand access token with padding bytes
    for(int i = 0, j = 0; i < dataSize; i += 2, j++) {
        pAccToken->data[i] = accessToken[j];
        pAccToken->data[i+1] = 0;
    }
    ...
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_ACCESS_TOKEN, (SQLPOINTER)pAccToken, SQL_IS_POINTER);
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);      
    ...
    free(pAccToken);
~~~
Di seguito è una stringa di connessione di esempio per l'uso con autenticazione Azure Active Directory Interactive. Si noti che non contiene campi PWD quando viene immessa la password utilizzando la schermata di autenticazione di Windows Azure.
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~

## <a name="see-also"></a>Vedere anche
[Supporto dell'autenticazione basata su token per il database SQL di Azure usando l'autenticazione di Azure AD](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

