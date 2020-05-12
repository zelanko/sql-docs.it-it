---
title: Uso di Azure Active Directory con il driver ODBC
description: Microsoft ODBC Driver for SQL Server consente alle applicazioni ODBC di connettersi a un'istanza del database SQL di Azure usando Azure Active Directory.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b829cb837eafb1a47283d50ede3ee789471e5f7f
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886308"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Uso di Azure Active Directory con il driver ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>Scopo

Microsoft ODBC Driver for SQL Server con la versione 13.1 o successiva consente alle applicazioni ODBC di connettersi a un'istanza del database SQL di Azure usando un'identità federata in Azure Active Directory con nome utente e password, un token di accesso di Azure Active Directory, un'identità del servizio gestito di Azure Active Directory o l'autenticazione integrata di Windows (_solo driver Windows_). Per la versione 13.1 del driver ODBC, l'autenticazione del token di accesso di Azure Active Directory è _solo Windows_. Il driver ODBC versione 17 e successive supporta questa autenticazione in tutte le piattaforme (Windows, Linux e macOS). Una nuova autenticazione interattiva di Azure Active Directory con ID di accesso è stato introdotta nella versione 17.1 per Windows del driver ODBC. Un nuovo metodo di autenticazione dell'identità del servizio gestito di Azure Active Directory è stato aggiunto nella versione del driver ODBC 17.3.1.1 per le identità assegnate dall'utente e dal sistema. Tutte queste operazioni sono eseguite tramite l'utilizzo di nuove parole chiave per la stringa di connessione e DSN e di attributi di connessione.

> [!NOTE]
> Il driver ODBC in Linux e macOS supporta solo l'autenticazione di Azure Active Directory direttamente da Azure Active Directory. Se si usa l'autenticazione con nome utente/password di Azure Active Directory da un client Linux o macOS e la configurazione di Active Directory richiede che il client esegua l'autenticazione in un endpoint Active Directory Federation Services, l'autenticazione potrebbe non riuscire.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>Parole chiave della stringa di connessione e DSN nuovi e/o modificati

È possibile usare la parola chiave `Authentication` quando ci si connette con un DSN o una stringa di connessione per controllare la modalità di autenticazione. Il valore impostato nella stringa di connessione sostituisce il valore nel DSN, se specificato. Il _valore pre-attributo_ dell'impostazione `Authentication` è il valore calcolato in base ai valori della stringa di connessione e del DSN.

|Nome|Valori|Predefinito|Descrizione|
|-|-|-|-|
|`Authentication`|(non impostato), (stringa vuota), `SqlPassword`, `ActiveDirectoryPassword`, `ActiveDirectoryIntegrated`, `ActiveDirectoryInteractive`, `ActiveDirectoryMsi` |(non impostato)|Controlla la modalità di autenticazione.<table><tr><th>valore<th>Descrizione<tr><td>(non impostato)<td>Modalità di autenticazione determinata da altre parole chiave (opzioni di connessione legacy esistenti).<tr><td>(stringa vuota)<td>(Solo stringa di connessione). Eseguire l'override e annullare l'impostazione di un valore `Authentication` specificato nel DSN.<tr><td>`SqlPassword`<td>Eseguire l'autenticazione direttamente in un'istanza di SQL Server usando un nome utente e una password.<tr><td>`ActiveDirectoryPassword`<td>Eseguire l'autenticazione con un'identità di Azure Active Directory usando un nome utente e una password.<tr><td>`ActiveDirectoryIntegrated`<td>_Solo driver Windows_. Eseguire l'autenticazione con un'identità di Azure Active Directory usando l'autenticazione integrata.<tr><td>`ActiveDirectoryInteractive`<td>_Solo driver Windows_. Eseguire l'autenticazione con un'identità di Azure Active Directory usando l'autenticazione interattiva.<tr><td>`ActiveDirectoryMsi`<td>Eseguire l'autenticazione con un'identità di Azure Active Directory usando l'autenticazione dell'identità del servizio gestito. Per l'identità assegnata dall'utente, UID è impostato sull'ID oggetto dell'identità utente.</table>|
|`Encrypt`|(non impostato), `Yes`, `No`|(vedere la descrizione)|Controlla la crittografia per una connessione. Se il valore del pre-attributo dell'impostazione `Authentication` è diverso da _nessuno_ nel DSN o nella stringa di connessione, il valore predefinito è `Yes`. Diversamente, il valore predefinito è `No`. Se l'attributo `SQL_COPT_SS_AUTHENTICATION` sostituisce il valore del pre-attributo di `Authentication`, impostare in modo esplicito il valore di crittografia nel DSN, nella stringa di connessione o nell'attributo di connessione. Il valore del pre-attributo della crittografia è `Yes` se il valore è impostato su `Yes` nella stringa di connessione o nel DSN.|

## <a name="new-andor-modified-connection-attributes"></a>Attributi di connessione nuovi e/o modificati

Per supportare l'autenticazione di Azure Active Directory sono stati introdotti o modificati gli attributi di preconnessione seguenti. Quando un attributo di connessione ha una parola chiave della stringa di connessione o del DSN corrispondente e viene impostato, l'attributo di connessione ha la precedenza.

|Attributo|Type|Valori|Predefinito|Descrizione|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_AD_MSI`, `SQL_AU_RESET`|(non impostato)|Vedere la descrizione della parola chiave `Authentication` fornita in precedenza. `SQL_AU_NONE` viene specificato per sostituire esplicitamente un valore `Authentication` impostato nella stringa di connessione e/o nel DSN, mentre `SQL_AU_RESET` rimuove l'impostazione se è stato impostato, consentendo al valore del DSN o della stringa di connessione di avere la precedenza.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|Puntatore a `ACCESSTOKEN` o NULL|NULL|Se diverso da Null, specifica il token di accesso di Azure AD da usare. È un errore specificare un token di accesso e le parole chiave della stringa di connessione `UID`, `PWD`, `Trusted_Connection` o `Authentication` o gli attributi equivalenti. <br> **NOTA** La versione 13.1 del driver ODBC supporta questa operazione solo in _Windows_.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(vedere la descrizione)|Controlla la crittografia per una connessione. `SQL_EN_OFF` e `SQL_EN_ON` rispettivamente disabilitano e abilitano la crittografia. Se il valore del pre-attributo dell'impostazione `Authentication` è diverso da _nessuno_ o è impostato `SQL_COPT_SS_ACCESS_TOKEN` e `Encrypt` non è stato specificato nel DSN o nella stringa di connessione, il valore predefinito è `SQL_EN_ON`. Diversamente, il valore predefinito è `SQL_EN_OFF`. Se l'attributo di connessione `SQL_COPT_SS_AUTHENTICATION` è impostato su un valore diverso da _nessuno_, impostare in modo esplicito `SQL_COPT_SS_ENCRYPT` sul valore desiderato se `Encrypt` non è stato specificato nella stringa di connessione o nel DSN. Il valore effettivo di questo attributo determina [se verrà usata la crittografia per la connessione.](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|Non supportato con Azure Active Directory, poiché le modifiche delle password nelle entità di sicurezza di AAD non possono essere eseguite tramite una connessione ODBC. <br><br>In SQL Server 2005 è stata introdotta la scadenza della password per l'autenticazione di SQL Server. L'attributo `SQL_COPT_SS_OLDPWD` è stato aggiunto per consentire al client di specificare sia la vecchia password che la nuova per la connessione. Quando questa proprietà è impostata, il provider non userà il pool di connessioni per la prima connessione o per le connessioni successive, in quanto la stringa di connessione conterrà la "vecchia password" che è stata modificata.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_Deprecato_; in alternativa, usare `SQL_COPT_SS_AUTHENTICATION` impostato su `SQL_AU_AD_INTEGRATED`. <br><br>Forza l'utilizzo dell'autenticazione di Windows (Kerberos in Linux e macOS) per la convalida dell'accesso in fase di connessione al server. Quando viene usata l'autenticazione di Windows, il driver ignora i valori di ID utente e password specificati come parte dell'elaborazione di `SQLConnect`, `SQLDriverConnect` o `SQLBrowseConnect`.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Aggiunte all'interfaccia utente per Azure Active Directory (solo driver Windows)

La configurazione DSN e le interfacce utente di connessione del driver sono state migliorate con le opzioni aggiuntive necessarie per l'utilizzo dell'autenticazione con Azure AD.

### <a name="creating-and-editing-dsns-in-the-ui"></a>Creazione e modifica dei DSN nell'interfaccia utente

È possibile usare le nuove opzioni di autenticazione di Azure AD durante la creazione o la modifica di un DSN esistente usando l'interfaccia utente di installazione del driver:

`Authentication=ActiveDirectoryIntegrated` per l'autenticazione integrata di Azure Active Directory in SQL Azure

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword` per l'autenticazione con nome utente/password di Azure Active Directory in SQL Azure

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` per l'autenticazione interattiva di Azure Active Directory in SQL Azure

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword` per l'autenticazione con nome utente/password in SQL Server (Azure o altro)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes` per l'autenticazione integrata SSPI legacy di Windows

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

Le cinque opzioni corrispondono rispettivamente a `Trusted_Connection=Yes` (autenticazione integrata con solo SSPI Windows legacy esistente) e `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword`, `ActiveDirectoryPassword` e `ActiveDirectoryInteractive`.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>Prompt SQLDriverConnect (solo driver Windows)

La finestra di dialogo di richiesta visualizzata da SQLDriverConnect quando richiede le informazioni necessarie per completare la connessione contiene tre nuove opzioni per l'autenticazione di Azure AD:

![ServerLogin.png](windows/ServerLogin.png)

Queste opzioni corrispondono alle cinque opzioni disponibili nell'interfaccia utente di configurazione del DSN descritta in precedenza.

### <a name="example-connection-strings"></a>Esempi di stringhe di connessione
1. Autenticazione di SQL Server - sintassi legacy. Il certificato del server non viene convalidato e la crittografia viene usata solo se viene imposta dal server. Nome utente e password vengono passati nella stringa di connessione.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. Autenticazione SQL - nuova sintassi. Il client richiede la crittografia (il valore predefinito di `Encrypt` è `true`) e il certificato del server viene convalidato, indipendentemente dall'impostazione della crittografia (a meno che `TrustServerCertificate` non sia impostato su `true`). Nome utente e password vengono passati nella stringa di connessione.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Autenticazione integrata di Windows (Kerberos in Linux e macOS) tramite SSPI (in SQL Server o SQL IaaS) - sintassi corrente. Il certificato del server non viene convalidato, a meno che non venga usata la crittografia. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Solo driver Windows_). Autenticazione integrata di Windows tramite SSPI (se il database di destinazione è in SQL Server o SQL IaaS) - nuova sintassi. Il client richiede la crittografia (il valore predefinito di `Encrypt` è `true`) e il certificato del server viene convalidato, indipendentemente dall'impostazione della crittografia (a meno che `TrustServerCertificate` non sia impostato su `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. Autenticazione con nome utente/password di AAD (se il database di destinazione si trova nel database SQL di Azure). Il certificato del server viene convalidato, indipendentemente dall'impostazione della crittografia (a meno che `TrustServerCertificate` non sia impostato su `true`). Nome utente e password vengono passati nella stringa di connessione. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Solo driver Windows_). Autenticazione integrata di Windows tramite ADAL, che prevede il riscatto delle credenziali dell'account di Windows per un token di accesso emesso da AAD, presupponendo che il database di destinazione si trovi nel database SQL di Azure. Il certificato del server viene convalidato, indipendentemente dall'impostazione della crittografia (a meno che `TrustServerCertificate` non sia impostato su `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Solo driver Windows_). L'autenticazione interattiva di AAD usa la tecnologia Azure per l'autenticazione a più fattori per configurare la connessione. In questa modalità, specificando l'ID di accesso, viene attivata una finestra di dialogo di autenticazione di Azure che consente all'utente di immettere la password per completare la connessione. Il nome utente viene passato nella stringa di connessione.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

8. L'autenticazione con identità del servizio gestito di AAD usa l'identità assegnata dal sistema o assegnata dall'utente per l'autenticazione per configurare la connessione. Per l'identità assegnata dall'utente, UID è impostato sull'ID oggetto dell'identità utente.<br>
Per l'identità assegnata dal sistema,<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
Per l'identità assegnata dall'utente con ID oggetto uguale a myObjectId,<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE]
>- Quando si usano le opzioni di Active Directory con il driver ODBC di Windows ***prima*** della versione 17.4.2, assicurarsi di avere installato [Active Directory Authentication Library per SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072). Quando si usano i driver Linux e macOS, assicurarsi che `libcurl` sia stato installato. Per la versione del driver 17.2 e versioni successive, questa non è una dipendenza esplicita poiché non è necessaria per gli altri metodi di autenticazione o per le operazioni ODBC.
>- Per connettersi usando il nome utente e la password di un account SQL Server, è ora possibile usare la nuova opzione `SqlPassword`, che è consigliata in particolare per SQL Azure poiché abilita impostazioni predefinite della connessione più sicure.
>- Per connettersi usando il nome utente e la password di un account Azure Active Directory, specificare `Authentication=ActiveDirectoryPassword` nella stringa di connessione e le parole chiave `UID` e `PWD` rispettivamente con nome utente e password.
>- Per connettersi usando l'autenticazione integrata di Windows o di Active Directory (solo driver Windows), specificare `Authentication=ActiveDirectoryIntegrated` nella stringa di connessione. Il driver sceglierà automaticamente la modalità di autenticazione corretta. `UID` e `PWD` non devono essere specificati.
>- Per connettersi usando l'autenticazione interattiva di Active Directory (solo driver Windows), è necessario specificare `UID`.

## <a name="authenticating-with-an-access-token"></a>Autenticazione con un token di accesso

L'attributo di preconnessione `SQL_COPT_SS_ACCESS_TOKEN` consente l'utilizzo di un token di accesso ottenuto da Azure AD per l'autenticazione anziché di nome utente e password e ignora anche la negoziazione e il recupero di un token di accesso da parte del driver. Per usare un token di accesso, impostare l'attributo di connessione `SQL_COPT_SS_ACCESS_TOKEN` su un puntatore a una struttura `ACCESSTOKEN`:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

`ACCESSTOKEN` è una struttura a lunghezza variabile costituita da una _lunghezza_ di 4 byte seguita da byte _lunghezza_ di dati opachi che formano il token di accesso. A causa del modo in cui SQL Server gestisce i token di accesso, un token ottenuto tramite una risposta JSON [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) deve essere espanso in modo che ogni byte sia seguito da un byte di riempimento 0, simile a una stringa UCS-2 contenente solo caratteri ASCII. Il token tuttavia è un valore opaco e la lunghezza specificata, in byte, NON deve includere alcun carattere di terminazione Null. A causa dei vincoli di lunghezza e di formato considerevoli, questo metodo di autenticazione è disponibile solo a livello di codice tramite l'attributo di connessione `SQL_COPT_SS_ACCESS_TOKEN`. Non è disponibile alcun DSN o alcuna parola chiave della stringa di connessione corrispondente. La stringa di connessione non deve contenere le parole chiave `UID`, `PWD`, `Authentication` o `Trusted_Connection`.

> [!NOTE]
> La versione 13.1 del driver ODBC supporta questa autenticazione solo in _Windows_.

## <a name="azure-active-directory-authentication-sample-code"></a>Codice di esempio dell'autenticazione di Azure Active Directory

L'esempio seguente mostra il codice necessario per connettersi a SQL Server usando Azure Active Directory con le parole chiave di connessione. Si noti che non è necessario modificare il codice dell'applicazione. La stringa di connessione o il DSN, se usato, è l'unica modifica necessaria per usare AAD per l'autenticazione:
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);    
    ...
~~~
L'esempio seguente mostra il codice necessario per connettersi a SQL Server usando Azure Active Directory con l'autenticazione con token di accesso. In questo caso, è necessario modificare il codice dell'applicazione per elaborare il token di accesso e impostare l'attributo di connessione associato.
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
Di seguito è riportata una stringa di connessione di esempio da usare con l'autenticazione interattiva di Azure Active Directory. Si noti che non contiene il campo PWD poiché la password viene inserita usando la schermata di autenticazione di Azure.
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~
Di seguito è riportata una stringa di connessione di esempio da usare con l'autenticazione con identità del servizio gestito di Azure Active Directory. Si noti che l'UID è impostato sull'ID oggetto dell'identità utente per l'identità assegnata dall'utente.
~~~
// For system-assigned identity,
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};Authentication=ActiveDirectoryMsi"
...
// For user-assigned identity with object ID equals to myObjectId
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myObjectId;Authentication=ActiveDirectoryMsi"
~~~

## <a name="see-also"></a>Vedere anche

[Supporto dell'autenticazione basata su token per il database SQL di Azure tramite l'autenticazione di Azure AD](/archive/blogs/sqlsecurity/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)
