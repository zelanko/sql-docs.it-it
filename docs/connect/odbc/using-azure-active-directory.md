---
title: Utilizzo di Azure Active Directory con il driver ODBC | Microsoft Docs per SQL Server
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
ms.openlocfilehash: c0f9d73dace4e17d87e1c93da703786fc920b2fb
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176162"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Uso di Azure Active Directory con il driver ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>Scopo

Il Microsoft ODBC Driver for SQL Server con la versione 13,1 o successive consente alle applicazioni ODBC di connettersi a un'istanza di SQL Azure usando un'identità federata in Azure Active Directory con nome utente/password, un token di accesso Azure Active Directory, un'istanza di Azure Active Identità del servizio gestito della directory o autenticazione integrata di Windows (_solo driver Windows_). Per la versione 13,1 del driver ODBC, l'autenticazione del token di accesso Azure Active Directory è _solo Windows_. Il driver ODBC versione 17 e successive supporta questa autenticazione in tutte le piattaforme (Windows, Linux e Mac). Un nuovo Azure Active Directory autenticazione interattiva con ID di accesso è stato introdotto nella versione 17,1 per Windows del driver ODBC. Un nuovo metodo di autenticazione dell'identità del servizio gestito Azure Active Directory è stato aggiunto nella versione del driver ODBC 17.3.1.1 per le identità assegnate dall'utente e dal sistema. Tutti questi risultati vengono eseguiti tramite l'utilizzo di nuove parole chiave per la stringa di connessione e DSN, nonché gli attributi di connessione.

> [!NOTE]
> Il driver ODBC in Linux e macOS non supporta Active Directory Federation Services. Se si usa Azure Active Directory l'autenticazione con nome utente/password da un client Linux o macOS e la configurazione Active Directory include servizi federati, l'autenticazione potrebbe non riuscire.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>Parole chiave delle stringhe di connessione e DSN nuove e/o modificate

La `Authentication` parola chiave può essere usata per la connessione a un DSN o a una stringa di connessione per controllare la modalità di autenticazione. Il valore impostato nella stringa di connessione esegue l'override del DSN, se specificato. Il _valore pre-attributo_ dell' `Authentication` impostazione è il valore calcolato dalla stringa di connessione e dai valori DSN.

|Nome|Valori|Default|Descrizione|
|-|-|-|-|
|`Authentication`|(non impostato), (stringa vuota), `SqlPassword` `ActiveDirectoryPassword` `ActiveDirectoryIntegrated`,,, `ActiveDirectoryInteractive`,`ActiveDirectoryMsi` |(non impostato)|Controlla la modalità di autenticazione.<table><tr><th>valore<th>Descrizione<tr><td>(non impostato)<td>Modalità di autenticazione determinata da altre parole chiave (opzioni di connessione legacy esistenti).<tr><td>(stringa vuota)<td>Guida alla stringa di connessione Eseguire l'override di `Authentication` un valore impostato nel DSN.<tr><td>`SqlPassword`<td>Eseguire l'autenticazione direttamente a un'istanza di SQL Server usando un nome utente e una password.<tr><td>`ActiveDirectoryPassword`<td>Eseguire l'autenticazione con un'identità Azure Active Directory usando un nome utente e una password.<tr><td>`ActiveDirectoryIntegrated`<td>_Solo driver Windows_. Eseguire l'autenticazione con un'identità Azure Active Directory usando l'autenticazione integrata.<tr><td>`ActiveDirectoryInteractive`<td>_Solo driver Windows_. Eseguire l'autenticazione con un'identità Azure Active Directory usando l'autenticazione interattiva.<tr><td>`ActiveDirectoryMsi`<td>Eseguire l'autenticazione con Azure Active Directory identità usando l'autenticazione dell'identità del servizio gestito. Per l'identità assegnata dall'utente, UID è impostato sull'ID oggetto dell'identità utente.</table>|
|`Encrypt`|(non impostato), `Yes`, `No`|(vedere la descrizione)|Controlla la crittografia per una connessione. Se il valore pre-attributo dell' `Authentication` impostazione non è _None_ nel DSN o nella stringa di connessione, il valore predefinito `Yes`è. Diversamente, il valore predefinito è `No`. Se l'attributo `SQL_COPT_SS_AUTHENTICATION` sostituisce il valore pre-attributo di `Authentication`, impostare in modo esplicito il valore della crittografia nel DSN o nella stringa di connessione o nell'attributo di connessione. Il valore pre-attributo della crittografia è `Yes` se il valore è impostato su `Yes` nel DSN o nella stringa di connessione.|

## <a name="new-andor-modified-connection-attributes"></a>Attributi di connessione nuovi e/o modificati

Per supportare l'autenticazione Azure Active Directory, sono stati introdotti o modificati i seguenti attributi di connessione pre-connessione. Quando un attributo di connessione dispone di una stringa di connessione o di una parola chiave DSN corrispondente e viene impostato, l'attributo Connection ha la precedenza.

|attribute|Tipo|Valori|Default|Descrizione|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_AD_MSI`, `SQL_AU_RESET`|(non impostato)|Vedere la descrizione `Authentication` della parola chiave sopra. `SQL_AU_NONE`viene fornito per eseguire l'override esplicito di un `Authentication` valore impostato nella stringa di connessione e/o DSN, `SQL_AU_RESET` mentre consente di annullare l'impostazione dell'attributo se è stato impostato, consentendo al DSN o al valore della stringa di connessione di avere la precedenza.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|Puntatore a `ACCESSTOKEN` o null|NULL|Se diverso da null, specifica il token di accesso AzureAD da usare. Non è possibile specificare un token `UID`di accesso e anche `PWD` `Trusted_Connection`le parole chiave della stringa `Authentication` di connessione,, o o i relativi attributi equivalenti. <br> **Nota:** La versione 13,1 del driver ODBC supporta questa operazione solo in _Windows_.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(vedere la descrizione)|Controlla la crittografia per una connessione. `SQL_EN_OFF`e `SQL_EN_ON` disabilitano e abilitano rispettivamente la crittografia. Se il valore pre- `Authentication` attributo dell'impostazione non è _None_ o `SQL_COPT_SS_ACCESS_TOKEN` è impostato e `Encrypt` non è stato specificato nel DSN o nella stringa di connessione, il valore predefinito è `SQL_EN_ON`. Diversamente, il valore predefinito è `SQL_EN_OFF`. Se l'attributo `SQL_COPT_SS_AUTHENTICATION` Connection è impostato su Not _None_, impostare `SQL_COPT_SS_ENCRYPT` esplicitamente sul valore desiderato se `Encrypt` non è stato specificato nel DSN o nella stringa di connessione. Il valore effettivo di questo attributo controlla [se la crittografia verrà utilizzata per la connessione.](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|Non supportato con Azure Active Directory, perché le modifiche delle password alle entità AAD non possono essere eseguite tramite una connessione ODBC. <br><br>In SQL Server 2005 è stata introdotta la scadenza della password per l'autenticazione di SQL Server. L' `SQL_COPT_SS_OLDPWD` attributo è stato aggiunto per consentire al client di fornire sia la vecchia che la nuova password per la connessione. Quando questa proprietà è impostata, il provider non utilizzerà il pool di connessioni per la prima connessione o per le connessioni successive, in quanto la stringa di connessione conterrà la password precedente che è stata modificata.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_Deprecato_; utilizzare `SQL_COPT_SS_AUTHENTICATION` invece l' `SQL_AU_AD_INTEGRATED` impostazione su. <br><br>Impone l'uso dell'autenticazione di Windows (Kerberos in Linux e macOS) per la convalida dell'accesso all'account di accesso del server. Quando si utilizza l'autenticazione di Windows, il driver ignora i valori dell'identificatore utente e della password `SQLConnect`forniti `SQLDriverConnect`come parte `SQLBrowseConnect` dell'elaborazione di, o.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Aggiunte all'interfaccia utente per Azure Active Directory (solo driver Windows)

La configurazione DSN e le interfacce utente di connessione del driver sono state migliorate con le opzioni aggiuntive necessarie per l'utilizzo dell'autenticazione con Azure AD.

### <a name="creating-and-editing-dsns-in-the-ui"></a>Creazione e modifica di DSN nell'interfaccia utente

È possibile utilizzare le nuove opzioni di autenticazione del Azure AD durante la creazione o la modifica di un DSN esistente utilizzando l'interfaccia utente di installazione del driver:

`Authentication=ActiveDirectoryIntegrated` per l'autenticazione integrata di Azure Active Directory in SQL Azure

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword`per Azure Active Directory l'autenticazione con nome utente/password per SQL Azure

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

`Authentication=ActiveDirectoryInteractive` per l'autenticazione interattiva di Azure Active Directory in SQL Azure

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword`per l'autenticazione con nome utente/password per SQL Server (Azure o altro)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes`per l'autenticazione integrata SSPI legacy di Windows

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

Le cinque opzioni corrispondono a `Trusted_Connection=Yes` (autenticazione integrata esistente solo SSPI di Windows) e `ActiveDirectoryInteractive` `Authentication=` `ActiveDirectoryIntegrated`rispettivamente, `SqlPassword` `ActiveDirectoryPassword`, e.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>Prompt SQLDriverConnect (solo driver Windows)

La finestra di dialogo di richiesta visualizzata da SQLDriverConnect quando richiede le informazioni necessarie per completare la connessione contiene tre nuove opzioni per l'autenticazione Azure AD:

![ServerLogin.png](windows/ServerLogin.png)

Queste opzioni corrispondono agli stessi cinque disponibili nell'interfaccia utente di configurazione DSN precedente.

### <a name="example-connection-strings"></a>Esempi di stringhe di connessione
1. Autenticazione SQL Server-sintassi legacy. Il certificato del server non viene convalidato e la crittografia viene utilizzata solo se il server lo impone. Il nome utente e la password vengono passati nella stringa di connessione.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. Autenticazione SQL: nuova sintassi. Il client richiede la crittografia `Encrypt` (il valore predefinito è `true`) e il certificato del server viene convalidato, indipendentemente dall'impostazione della crittografia (a meno che non `TrustServerCertificate` sia impostato su `true`). Il nome utente e la password vengono passati nella stringa di connessione.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Autenticazione integrata di Windows (Kerberos in Linux e macOS) tramite SSPI (per SQL Server o SQL IaaS)-sintassi corrente. Il certificato del server non viene convalidato, a meno che non venga utilizzata la crittografia. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Solo driver Windows_). Autenticazione integrata di Windows tramite SSPI (se il database di destinazione è in SQL Server o SQL IaaS)-nuova sintassi. Il client richiede la crittografia `Encrypt` (il valore predefinito è `true`) e il certificato del server viene convalidato, indipendentemente dall'impostazione della crittografia (a meno che non `TrustServerCertificate` sia impostato su `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. Autenticazione con nome utente/password di AAD (se il database di destinazione si trova nel database SQL di Azure). Il certificato del server viene convalidato, indipendentemente dall'impostazione della crittografia `TrustServerCertificate` (a meno `true`che non sia impostato su). Il nome utente e la password vengono passati nella stringa di connessione. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Solo driver Windows_). Autenticazione integrata di Windows tramite ADAL, che prevede il riscatto delle credenziali dell'account di Windows per un token di accesso emesso da AAD, presupponendo che il database di destinazione si trovi nel database SQL di Azure. Il certificato del server viene convalidato, indipendentemente dall'impostazione della crittografia `TrustServerCertificate` (a meno `true`che non sia impostato su). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Solo driver Windows_). L'autenticazione interattiva di AAD usa la tecnologia Azure per l'autenticazione a più fattori per configurare la connessione. In questa modalità, fornendo l'ID di accesso, viene attivata una finestra di dialogo di autenticazione di Azure che consente all'utente di immettere la password per completare la connessione. Il nome utente viene passato nella stringa di connessione.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

8. L'autenticazione identità del servizio gestita di AAD usa l'identità assegnata dal sistema o assegnata dall'utente per l'autenticazione per configurare la connessione. Per l'identità assegnata dall'utente, UID è impostato sull'ID oggetto dell'identità utente.<br>
Per l'identità assegnata dal sistema,<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
Per l'identità assegnata dall'utente con ID oggetto uguale a myObjectId,<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE] 
>- Quando si utilizzano le nuove opzioni di Active Directory con il driver ODBC di Windows, verificare che sia stato installato il [Active Directory Authentication Library per SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) . Quando si usano i driver Linux e MacOS, verificare `libcurl` che sia stato installato. Per la versione del driver 17,2 e versioni successive, questa non è una dipendenza esplicita perché non è necessaria per gli altri metodi di autenticazione o per le operazioni ODBC.
>- Per connettersi usando un nome utente e una password di account SQL Server, è ora possibile `SqlPassword` usare la nuova opzione, che è consigliata in particolare per SQL Azure perché questa opzione Abilita le impostazioni predefinite di connessione più sicure.
>- Per connettersi usando un nome utente e una password di account `Authentication=ActiveDirectoryPassword` Azure Active Directory, specificare rispettivamente nella stringa `UID` di `PWD` connessione e le parole chiave e con il nome utente e la password.
>- Per connettersi utilizzando l'autenticazione integrata di Windows o Active Directory (solo driver Windows), `Authentication=ActiveDirectoryIntegrated` specificare nella stringa di connessione. Il driver sceglierà automaticamente la modalità di autenticazione corretta. `UID`e `PWD` non devono essere specificati.
>- Per connettersi utilizzando Active Directory autenticazione interattiva (solo driver Windows), `UID` è necessario specificare.

## <a name="authenticating-with-an-access-token"></a>Autenticazione con un token di accesso

L' `SQL_COPT_SS_ACCESS_TOKEN` attributo pre-Connection consente l'uso di un token di accesso ottenuto da Azure ad per l'autenticazione anziché nome utente e password e ignora inoltre la negoziazione e il recupero di un token di accesso da parte del driver. Per usare un token di accesso, impostare `SQL_COPT_SS_ACCESS_TOKEN` l'attributo di connessione su un puntatore `ACCESSTOKEN` a una struttura:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

È una struttura a lunghezza variabile costituita da una _lunghezza_ di 4 byte seguita da byte di _lunghezza_ di dati opachi che formano il token di accesso. `ACCESSTOKEN` A causa del modo in cui SQL Server gestisce i token di accesso, è necessario espandere uno ottenuto tramite una risposta JSON [OAuth 2,0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) in modo che ogni byte sia seguito da un byte di riempimento 0, simile a una stringa UCS-2 contenente solo caratteri ASCII; Tuttavia, il token è un valore opaco e la lunghezza specificata, in byte, non deve includere alcun carattere di terminazione null. A causa dei vincoli di lunghezza e di formato considerevoli, questo metodo di autenticazione è disponibile solo a `SQL_COPT_SS_ACCESS_TOKEN` livello di codice tramite l'attributo Connection. non esiste alcuna parola chiave corrispondente DSN o della stringa di connessione. La stringa di connessione non deve `UID`contenere `PWD`parole `Authentication`chiave, `Trusted_Connection` , o.

> [!NOTE]
> La versione 13,1 del driver ODBC supporta questa autenticazione solo in _Windows_.

## <a name="azure-active-directory-authentication-sample-code"></a>Codice di esempio dell'autenticazione di Azure Active Directory

Nell'esempio seguente viene illustrato il codice necessario per connettersi a SQL Server utilizzando Azure Active Directory con le parole chiave di connessione. Si noti che non è necessario modificare il codice dell'applicazione. la stringa di connessione, o DSN se ne viene usato uno, è l'unica modifica necessaria per usare AAD per l'autenticazione:
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
Nell'esempio seguente viene illustrato il codice necessario per connettersi a SQL Server tramite Azure Active Directory con l'autenticazione del token di accesso. In questo caso, è necessario modificare il codice dell'applicazione per elaborare il token di accesso e impostare l'attributo di connessione associato.
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
Di seguito è riportata una stringa di connessione di esempio da utilizzare con Azure Active Directory l'autenticazione interattiva. Si noti che non contiene il campo PWD perché la password viene immessa usando la schermata di autenticazione di Azure.
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~
Di seguito è riportata una stringa di connessione di esempio per l'uso con l'autenticazione Azure Active Directory identità del servizio gestita. Si noti che l'UID è impostato sull'ID oggetto dell'identità utente per l'identità assegnata dall'utente.
~~~
// For system-assigned identity,
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};Authentication=ActiveDirectoryMsi"
...
// For user-assigned identity with object ID equals to myObjectId
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myObjectId;Authentication=ActiveDirectoryMsi"
~~~

## <a name="see-also"></a>Vedere anche
[Supporto dell'autenticazione basata su token per il database SQL di Azure con Azure AD auth](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

