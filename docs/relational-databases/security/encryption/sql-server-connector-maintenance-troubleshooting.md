---
title: Manutenzione e risoluzione dei problemi del Connettore SQL Server
description: Informazioni sulle istruzioni di manutenzione e i passaggi comuni per la risoluzione dei problemi per il Connettore SQL Server.
ms.custom: seo-lt-2019
ms.date: 07/25/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, appendix
ms.assetid: 7f5b73fc-e699-49ac-a22d-f4adcfae62b1
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 050b6ba215d9dc4db433ad81dd8fa48bed212803
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "75557936"
---
# <a name="sql-server-connector-maintenance--troubleshooting"></a>Manutenzione e risoluzione dei problemi del Connettore SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Informazioni supplementari sul Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono disponibili in questo argomento. Per altre informazioni sul Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [Extensible Key Management con l'insieme di credenziali delle chiavi di Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md), [Procedura di installazione di Extensible Key Management con l'insieme di credenziali delle chiavi di Azure](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md) e [Usare Connettore SQL Server con le funzionalità di crittografia SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md).  
  
  
##  <a name="a-maintenance-instructions-for-ssnoversion-connector"></a><a name="AppendixA"></a> A. Istruzioni di manutenzione per Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
### <a name="key-rollover"></a>Rollover della chiave  
  
> [!IMPORTANT]  
>  Il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] richiede che nel nome della chiave vengano usati solo i caratteri "a-z", "A-Z", "0-9" e "-", con un limite di 26 caratteri.   
> Versioni diverse della chiave con lo stesso nome di chiave nell'insieme di credenziali delle chiavi di Azure non funzioneranno con il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per ruotare una chiave di Azure Key Vault usata da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è necessario creare una nuova chiave con un nuovo nome.  
  
 In genere, il controllo delle versioni delle chiavi asimmetriche del server per la crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve essere eseguito ogni 1-2 anni. È importante notare che, anche se l'insieme di credenziali delle chiavi consente il controllo delle versioni delle chiavi, i clienti non dovrebbero usare questa funzionalità per implementare il controllo delle versioni. Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non può gestire le modifiche alla versione della chiave nell'insieme di credenziali delle chiavi. Per implementare il controllo delle versioni delle chiavi, è necessario che il cliente crei una nuova chiave nell'insieme di credenziali delle chiavi e quindi crittografi di nuovo la chiave di crittografia dei dati in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
 Ecco come si ottiene questo risultato per TDE:  
  
-   **In PowerShell:** creare una nuova chiave asimmetrica (con un nome diverso dalla chiave asimmetrica TDE corrente) nell'insieme di credenziali delle chiavi.  
  
    ```powershell  
    Add-AzKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'Key2' -Destination 'Software'  
    ```  
  
-   **Uso di [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] o sqlcmd.exe:** usare le istruzioni seguenti, come illustrato nella sezione 3 del passaggio 3.  
  
     Importare la nuova chiave asimmetrica.  
  
    ```sql  
    USE master  
    CREATE ASYMMETRIC KEY [MASTER_KEY2]   
    FROM PROVIDER [EKM]   
    WITH PROVIDER_KEY_NAME = 'Key2',   
    CREATION_DISPOSITION = OPEN_EXISTING   
    GO  
    ```  
  
     Creare un nuovo account di accesso da associare alla nuova chiave asimmetrica (come illustrato nelle istruzioni relative a TDE).  
  
    ```sql  
    USE master  
    CREATE LOGIN TDE_Login2   
    FROM ASYMMETRIC KEY [MASTER_KEY2]  
    GO  
    ```  
  
     Creare nuove credenziali per il mapping all'account di accesso.  
  
    ```sql  
    CREATE CREDENTIAL Azure_EKM_TDE_cred2  
        WITH IDENTITY = 'ContosoDevKeyVault',   
       SECRET = 'EF5C8E094D2A4A769998D93440D8115DAADsecret123456789='   
    FOR CRYPTOGRAPHIC PROVIDER EKM;  
  
    ALTER LOGIN TDE_Login2  
    ADD CREDENTIAL Azure_EKM_TDE_cred2;  
    GO  
    ```  
  
     Scegliere il database per cui si vuole crittografare di nuovo la chiave di crittografia del database.  
  
    ```sql  
    USE [database]  
    GO  
    ```  
  
     Crittografare di nuovo la chiave di crittografia del database.  
  
    ```sql  
    ALTER DATABASE ENCRYPTION KEY   
    ENCRYPTION BY SERVER ASYMMETRIC KEY [MASTER_KEY2];  
    GO  
    ```  
  
### <a name="upgrade-of-ssnoversion-connector"></a>Aggiornamento del Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

Le versioni 1.0.0.440 e precedenti sono state sostituite e non sono più supportate negli ambienti di produzione. Le versioni 1.0.1.0 e successive sono supportate negli ambienti di produzione. Usare le istruzioni seguenti per eseguire l'aggiornamento alla versione più recente disponibile nell'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=45344).

Se è in uso la versione 1.0.1.0 o una versione successiva, seguire questa procedura per eseguire l'aggiornamento alla versione più recente del Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Queste istruzioni evitano di dover riavviare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .
 
1. Installare la versione più recente del Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dall' [Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=45344). Nell'installazione guidata salvare il nuovo file DLL in un percorso di file diverso dal percorso del file DLL del Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] originale. Il nuovo percorso di file potrebbe ad esempio essere: `C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll`
 
2. Nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]eseguire il comando Transact-SQL seguente per fare in modo che l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] punti alla nuova versione del Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :

    ``` 
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll'
    GO  
    ```

Se è in uso la versione 1.0.0.440 o una versione precedente, seguire questa procedura per eseguire l'aggiornamento alla versione più recente del Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .
  
1.  Arrestare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
2.  Arrestare il servizio del Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
3.  Disinstallare Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando Programmi e funzionalità di Windows.  
  
     In alternativa, è possibile rinominare la cartella in cui si trova il file DLL. Il nome predefinito della cartella è "[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per Microsoft Azure Key Vault".  
  
4.  Installare la versione più recente del Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dall'Area download Microsoft.  
  
5.  Riavviare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
6.  Eseguire questa istruzione per modificare il provider EKM per iniziare a usare la versione più recente del Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Assicurarsi che il percorso file punti alla posizione in cui è stata scaricata la versione più recente. È possibile ignorare questo passaggio se la nuova versione viene installata nello stesso percorso della versione originale. 
  
    ```sql  
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
7.  Verificare che i database che usano TDE siano accessibili.  
  
8.  Dopo aver verificato il corretto funzionamento dell'aggiornamento, è possibile eliminare la cartella precedente di Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se si è scelto di rinominarla invece di disinstallarla nel passaggio 3.  
  
### <a name="rolling-the-ssnoversion-service-principal"></a>Rollover dell'entità servizio di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa le entità servizio create in Azure Active Directory come credenziali per accedere all'insieme di credenziali delle chiavi.  L'entità servizio ha un ID client e una chiave di autenticazione.  Le credenziali di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono configurate con il **nome dell'insieme di credenziali**, l' **ID client**e la **chiave di autenticazione**.  La **Chiave di autenticazione** è valida per un determinato periodo di tempo (uno o due anni).   Prima della scadenza è necessario generare una nuova chiave in Azure AD per l'entità servizio.  Successivamente è necessario cambiare le credenziali in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].    [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] mantiene una cache per le credenziali nella sessione corrente, per cui, quando vengono modificate le credenziali, [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] deve essere riavviato.  
  
### <a name="key-backup-and-recovery"></a>Backup e ripristino delle chiavi  
È importante eseguire regolarmente il backup dell'insieme di credenziali delle chiavi. In caso di perdita di una chiave asimmetrica nell'insieme di credenziali, è possibile ripristinarla dal backup. La chiave deve essere ripristinata usando lo stesso nome precedente con il comando Restore di PowerShell (vedere i passaggi successivi).  
In caso di perdita dell'insieme di credenziali, è necessario ricreare un insieme di credenziali e ripristinare la chiave asimmetrica al suo interno usando lo stesso nome assegnato in precedenza. Il nome dell'insieme di credenziali può essere diverso o uguale rispetto a prima. È necessario impostare anche le autorizzazioni di accesso nel nuovo insieme di credenziali per concedere all'entità servizio di SQL Server l'accesso richiesto per gli scenari di crittografia di SQL Server e quindi modificare le credenziali di SQL Server in modo che includano il nuovo nome dell'insieme di credenziali.

In sintesi, ecco i passaggi necessari:  
  
* Eseguire il backup della chiave dell'insieme di credenziali usando il cmdlet di Powershell Backup-AzureKeyVaultKey.  
* In caso di errore dell'insieme di credenziali, crearne uno nuovo nella stessa area geografica*. L'utente che lo crea deve trovarsi nella stessa directory predefinita dell'entità servizio configurata per SQL Server.  
* Ripristinare la chiave nel nuovo insieme di credenziali usando il cmdlet di Powershell Restore-AzureKeyVaultKey che consente di ripristinare la chiave usando lo stesso nome che aveva in precedenza. Se esiste già una chiave con lo stesso nome, il ripristino non riesce.  
* Concedere le autorizzazioni all'entità servizio di SQL Server per l'uso di questo nuovo insieme di credenziali.  
* Modificare le credenziali di SQL Server usate dal motore di database in modo da riflettere il nuovo nome dell'insieme di credenziali, se necessario.  
  
I backup delle chiavi possono essere ripristinati nelle aree di Azure, a condizione che rimangano nella stessa area geografica o nel cloud nazionale: Stati Uniti, Canada, Giappone, Australia, India, Asia Pacifico, Europa, Brasile, Cina, US Gov o Germania.  
  
  
##  <a name="b-frequently-asked-questions"></a><a name="AppendixB"></a> B. Domande frequenti  
### <a name="on-azure-key-vault"></a>Informazioni sull'insieme di credenziali delle chiavi di Azure  
  
**Come funzionano le operazioni relative alla chiave nell'insieme di credenziali delle chiavi di Azure?**  
 la chiave asimmetrica nell'insieme di credenziali delle chiavi viene usata per proteggere le chiavi di crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Solo la parte pubblica della chiave asimmetrica lascia sempre l'insieme di credenziali. La parte privata non viene mai esportata dall'insieme di credenziali. Tutte le operazioni di crittografia che usano la chiave asimmetrica vengono eseguite all'interno del servizio Azure Key Vault e sono protette dal sistema di sicurezza del servizio.  
  
 **Che cos'è un URI della chiave?**  
 Ogni chiave nell'insieme di credenziali delle chiavi di Azure ha un URI (Uniform Resource Identifier) che può essere usato per fare riferimento alla chiave dell'applicazione. Usare il formato `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey` per ottenere la versione corrente e usare il formato `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87` per ottenere una versione specifica.  
  
### <a name="on-configuring-ssnoversion"></a>Informazioni sulla configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

**Quali sono gli endpoint a cui deve accedere Connettore SQL Server?** Il connettore comunica con due endpoint che devono essere inclusi nell'elenco degli elementi consentiti. L'unica porta necessaria per la comunicazione in uscita a questi altri servizi è 443 per Https:
-  login.microsoftonline.com/*:443
-  *.vault.azure.net/* :443

**Come si esegue la connessione ad Azure Key Vault usando un server proxy HTTP(S)?**
Il Connettore usa le impostazioni di configurazione del proxy di Internet Explorer. Queste impostazioni possono essere controllate usando [Criteri di gruppo](https://blogs.msdn.microsoft.com/askie/2015/10/12/how-to-configure-proxy-settings-for-ie10-and-ie11-as-iem-is-not-available/) o il Registro di sistema, ma è importante tenere presente che non sono impostazioni a livello di sistema e dovranno essere indirizzate all'account del servizio che esegue l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se un amministratore del database visualizza o modifica le impostazioni in Internet Explorer, queste avranno effetto solo sull'account dell'amministratore del database anziché sul motore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. L'accesso interattivo al server usando l'account del servizio non è consigliato e viene bloccato in molti ambienti protetti. Per rendere effettive le modifiche apportate alle impostazioni proxy configurate, può essere necessario riavviare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] perché vengono memorizzate nella cache quando il Connettore tenta per la prima volta di connettersi a un insieme di credenziali delle chiavi.

**Quali sono i livelli minimi di autorizzazione necessari per ogni passaggio di configurazione in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]?**  
 Anche se è possibile eseguire tutti i passaggi di configurazione come membro del ruolo predefinito del server sysadmin, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] consiglia di ridurre al minimo le autorizzazioni. L'elenco seguente indica il livello di autorizzazione minima per ogni azione.  
  
-   Per creare un provider di crittografia è necessaria l'autorizzazione `CONTROL SERVER` o l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
-   Per modificare un'opzione di configurazione ed eseguire l'istruzione `RECONFIGURE` , è necessaria l'autorizzazione a livello di server `ALTER SETTINGS` . L'autorizzazione `ALTER SETTINGS` è assegnata implicitamente ai ruoli predefiniti del server sysadmin e **serveradmin** .  
  
-   Per creare le credenziali è necessaria l'autorizzazione `ALTER ANY CREDENTIAL` .  
  
-   Per aggiungere le credenziali a un account di accesso è necessaria l'autorizzazione `ALTER ANY LOGIN` .  
  
-   Per creare una chiave asimmetrica è necessaria l'autorizzazione `CREATE ASYMMETRIC KEY` .  

**Come è possibile cambiare l'istanza predefinita di Active Directory in modo che l'insieme di credenziali delle chiavi venga creato nella stessa sottoscrizione dell'entità servizio di Active Directory creata per il Connettore [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] ?**

![aad-change-default-directory-helpsteps](../../../relational-databases/security/encryption/media/aad-change-default-directory-helpsteps.png)

1. Andare al portale di Azure classico: [https://manage.windowsazure.com](https://manage.windowsazure.com)  
2. Nel menu a sinistra scorrere verso il basso e selezionare **Impostazioni**.
3. Selezionare la sottoscrizione di Azure attualmente in uso e fare clic su **Modifica directory** nei comandi nella parte inferiore della schermata.
4. Nella finestra popup usare il menu a discesa **Directory** per selezionare l'istanza di Active Directory che si vuole usare. L'istanza verrà impostata come directory predefinita.
5. Assicurarsi di essere l'amministratore globale della nuova istanza di Active Directory selezionata. Se non si è l'amministratore globale, si potrebbero perdere le autorizzazioni di gestione a causa della modifica della directory.
6. Dopo la chiusura della finestra popup, se non è visualizzata alcuna sottoscrizione, potrebbe essere necessario aggiornare il filtro **Filtra per directory** in **Sottoscrizioni** nel menu in alto a destra della schermata per visualizzare le sottoscrizioni che usano l'istanza di Active Directory appena aggiornata.

    > [!NOTE] 
    > Si potrebbe non disporre delle autorizzazioni per modificare la directory predefinita nella sottoscrizione di Azure. In questo caso, creare l'entità servizio AAD nella directory predefinita, in modo che si trovi nella stessa directory dell'insieme di credenziali delle chiavi di Azure usato successivamente.

Per altre informazioni su Active Directory, leggere [Associare le sottoscrizioni di Azure ad Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-how-subscriptions-associated-directory/).
  
##  <a name="c-error-code-explanations-for-ssnoversion-connector"></a><a name="AppendixC"></a> C. Spiegazioni dei codici di errore per Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 **Codici di errore del provider:**  
  
Codice di errore  |Simbolo  |Descrizione    
---------|---------|---------  
0 | scp_err_Success | L'operazione è stata completata.    
1 | scp_err_Failure | L'operazione non è riuscita.    
2 | scp_err_InsufficientBuffer | Questo errore indica al motore di allocare altra memoria per il buffer.    
3 | scp_err_NotSupported | L'operazione non è supportata. Ad esempio, il tipo di chiave o l'algoritmo specificato non è supportato dal provider EKM.    
4 | scp_err_NotFound | Il provider EKM non ha trovato la chiave o l'algoritmo specificato.    
5 | scp_err_AuthFailure | L'autenticazione con il provider EKM non è riuscita.    
6 | scp_err_InvalidArgument | L'argomento specificato non è valido.    
7 | scp_err_ProviderError | Si è verificato un errore non specificato nel provider EKM rilevato dal motore SQL.   
401 | acquireToken | Il server ha restituito 401 per la richiesta. Verificare che l'ID client e il segreto siano corretti e che la stringa delle credenziali sia una concatenazione dell'ID client e del segreto di AAD senza trattini.
404 | getKeyByName | Il server ha risposto 404, perché il nome della chiave non è stato trovato. Assicurarsi che il nome della chiave sia presente nell'insieme di credenziali.
2049 | scp_err_KeyNameDoesNotFitThumbprint | Il nome della chiave è troppo lungo per il sistema di identificazione personale del motore SQL. Il nome della chiave non deve superare i 26 caratteri.    
2050 | scp_err_PasswordTooShort | La stringa del segreto, che rappresenta la concatenazione dell'ID client e del segreto di AAD, contiene un numero di caratteri inferiore a 32.    
2051 | scp_err_OutOfMemory | La memoria del motore SQL è insufficiente e non è stato possibile allocare memoria per il provider EKM.    
2052 | scp_err_ConvertKeyNameToThumbprint | La conversione del nome della chiave in identificazione personale non è riuscita.    
2053 | scp_err_ConvertThumbprintToKeyName|  La conversione dell'identificazione personale nel nome della chiave non è riuscita.    
3000 | ErrorSuccess | L'operazione AKV è stata completata.    
3001 | ErrorUnknown | L'operazione AKV non è riuscita con un errore non specificato.    
3002 | ErrorHttpCreateHttpClientOutOfMemory | Non è possibile creare HttpClient per un'operazione AKV perché la memoria è insufficiente.    
3003 | ErrorHttpOpenSession | Impossibile aprire una sessione HTTP a causa di un errore di rete.    
3004 | ErrorHttpConnectSession | Impossibile connettere una sessione HTTP a causa di un errore di rete.    
3005 | ErrorHttpAttemptConnect | Impossibile tentare la connessione a causa di un errore di rete.    
3006 | ErrorHttpOpenRequest | Non è possibile aprire una richiesta a causa di un errore di rete.    
3007 | ErrorHttpAddRequestHeader | Non è possibile aggiungere l'intestazione della richiesta.    
3008 | ErrorHttpSendRequest | Non è possibile inviare una richiesta a causa di un errore di rete.    
3009 | ErrorHttpGetResponseCode | Non è possibile ottenere un codice di risposta a causa di un errore di rete.    
3010 | ErrorHttpResponseCodeUnauthorized | Il server ha restituito 401 per la richiesta.    
3011 | ErrorHttpResponseCodeThrottled | Il server ha limitato la richiesta.    
3012 | ErrorHttpResponseCodeClientError | La richiesta inviata dal connettore non è valida. Questo significa in genere che il nome della chiave non è valido o contiene caratteri non validi.
3013 | ErrorHttpResponseCodeServerError | Il server ha restituito un codice di risposta compreso tra 500 e 600.    
3014 | ErrorHttpQueryHeader | Non è possibile eseguire la query per un'intestazione della risposta.    
3015 | ErrorHttpQueryHeaderOutOfMemoryCopyHeader | Non è possibile copiare l'intestazione della risposta a causa della memoria insufficiente.    
3016 | ErrorHttpQueryHeaderOutOfMemoryReallocBuffer | Non è possibile eseguire la query sull'intestazione della risposta a causa della memoria insufficiente durante la riallocazione di un buffer.    
3017 | ErrorHttpQueryHeaderNotFound | Non è possibile trovare l'intestazione della query nella risposta.    
3018 | ErrorHttpQueryHeaderUpdateBufferLength | Non è possibile aggiornare la lunghezza del buffer quando si eseguono query sull'intestazione della risposta.    
3019 | ErrorHttpReadData | Non è possibile leggere i dati della risposta a causa di un errore di rete. 
3076 | ErrorHttpResourceNotFound | Il server ha risposto 404, perché il nome della chiave non è stato trovato. Assicurarsi che il nome della chiave sia presente nell'insieme di credenziali.
3077 | ErrorHttpOperationForbidden | Il server ha restituito l'errore 403 perché l'utente non ha le autorizzazioni appropriate per eseguire l'azione. Assicurarsi di avere le autorizzazioni per l'operazione specificata. Per il corretto funzionamento, il connettore richiede almeno le autorizzazioni "get, list, wrapKey, unwrapKey".   
  
Se il codice di errore non è presente in questa tabella, di seguito sono riportate alcune altre condizioni che potrebbero essere causa dell'errore:   
  
-   Non si ha accesso a Internet, quindi non è possibile accedere ad Azure Key Vault. Verificare la connessione Internet.  
  
-   Il servizio dell'insieme di credenziali delle chiavi potrebbe non essere attivo. Riprovare in un altro momento.  
  
-   La chiave asimmetrica dell'insieme di credenziali delle chiavi di Azure o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]potrebbe essere stata eliminata. Ripristinare la chiave.  
  
-   Se viene visualizzato l'errore "Impossibile caricare la libreria", verificare che sia installata la versione di Visual Studio C++ Redistributable appropriata in base alla versione di SQL Server in esecuzione. La tabella seguente specifica la versione da installare dall'Area download Microsoft.   

Nel registro eventi di Windows vengono inoltre registrati gli errori associati al Connettore SQL Server e questo può essere utile per avere maggiori informazioni sul motivo per cui si sta verificando l'errore. L'origine nel log eventi dell'applicazione di Windows sarà "Connettore SQL Server per Azure Key Vault".
  
Versione di SQL Server  |Collegamento di installazione ridistribuibile    
---------|--------- 
2008, 2008 R2, 2012, 2014 | [Visual C++ Redistributable Package per Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Visual C++ Redistributable per Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48145)    
  
  
## <a name="additional-references"></a>Riferimenti aggiuntivi  
 Altre informazioni su Extensible Key Management:  
  
-   [Extensible Key Management &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
 Crittografie di SQL che supportano EKM:  
  
-   [Abilitare TDE in SQL Server con EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
-   [Crittografia dei backup](../../../relational-databases/backup-restore/backup-encryption.md)  
  
-   [Creare un backup crittografato](../../../relational-databases/backup-restore/create-an-encrypted-backup.md)  
  
 Comandi di [!INCLUDE[tsql](../../../includes/tsql-md.md)] correlati:  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
 Documentazione dell'insieme di credenziali delle chiavi di Azure:  
  
-   [Cos'è l'insieme di credenziali chiave di Azure?](https://azure.microsoft.com/documentation/articles/key-vault-whatis/)  
  
-   [Introduzione all'insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)  
  
-   Riferimento di PowerShell [Cmdlet per l'insieme di credenziali delle chiavi di Azure](/powershell/module/azurerm.keyvault/)  
  
## <a name="see-also"></a>Vedere anche

 [Extensible Key Management tramite l'insieme di credenziali delle chiavi di Azure](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [Usare Connettore SQL Server con le funzionalità di crittografia SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)  
 [Opzione di configurazione del server EKM provider enabled](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
 [Procedura di installazione di Extensible Key Management con l'insieme di credenziali delle chiavi di Azure](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)
