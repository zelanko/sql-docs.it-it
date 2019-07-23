---
title: Configurare Always Encrypted usando SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f9ceeb515aa88e3b86be1732ff3f617eea31156c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050034"
---
# <a name="configure-always-encrypted-using-sql-server-management-studio"></a>Configure Always Encrypted using SQL Server Management Studio (Configurare Always Encrypted usando SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Questo articolo descrive le operazioni necessarie per la configurazione di Always Encrypted e la gestione dei database che usano Always Encrypted con [SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md).

Quando viene usato per configurare Always Encrypted, SSMS gestisce sia le chiavi che i dati sensibili di Always Encrypted in modo tale che vengano visualizzati in testo non crittografato all'interno del processo di SSMS. È quindi importante eseguire SSMS in un computer protetto. Se il database è ospitato in SQL Server, verificare che SSMS venga eseguito in un computer diverso da quello che ospita l'istanza di SQL Server. Poiché l'obiettivo principale di Always Encrypted è garantire la sicurezza dei dati sensibili crittografati anche se il sistema di database viene compromesso, eseguire uno script di PowerShell che elabora le chiavi o i dati sensibili nel computer SQL Server può ridurre o annullare i vantaggi della funzionalità. Per altre indicazioni, vedere [Considerazioni sulla sicurezza per la gestione delle chiavi](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management).

SQL Server Management Studio non supporta la separazione dei ruoli tra quelli che gestiscono il database (DBA) e quelli che gestiscono i segreti di crittografia e hanno accesso ai dati in testo normale (amministratori della sicurezza e/o di applicazioni). Se l'organizzazione applica la separazione dei ruoli, è necessario usare PowerShell per configurare Always Encrypted. Per altre informazioni, vedere [Panoramica della gestione delle chiavi per Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) e [Configurare Always Encrypted con PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).

## <a name="configuring-always-encrypted-using-the-always-encrypted-wizard"></a>Configurazione di Always Encrypted con la relativa procedura guidata

La [procedura guidata di Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md) è un potente strumento che consente di impostare la configurazione di crittografia per le colonne di database selezionate. In base alla configurazione corrente di Always Encrypted e alla configurazione di destinazione desiderata, la procedura guidata è in grado di crittografare una colonna, rimuovere la crittografia o riapplicarla, ad esempio una nuova chiave di crittografia della colonna o un tipo di crittografia diverso da quello in uso, configurato per la colonna. È possibile configurare più colonne in una singola sessione della procedura guidata.

Se non è stato eseguito il provisioning tutte le chiavi per Always Encrypted, la procedura guidata le genera automaticamente. Scegliere semplicemente un archivio chiavi per la chiave master della colonna: Archivio certificati Windows o Azure Key Vault. La procedura guidata genererà automaticamente i nomi per le chiavi e i relativi oggetti di metadati nel database. Per avere un maggiore controllo sulla modalità di provisioning delle chiavi e più possibilità di scelta per un archivio chiavi contenente una chiave master della colonna, è possibile usare le finestre di dialogo **Nuova chiave master della colonna** e **Nuova chiave di crittografia della colonna** (descritte di seguito) per eseguire il provisioning delle chiavi prima di iniziare la procedura guidata. Nella procedura guidata di Always Encrypted è possibile scegliere la chiave di crittografia esistente per la colonna.

Per informazioni dettagliate sull'uso della procedura guidata, vedere  [Procedura guidata di Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md).

## <a name="querying-encrypted-columns"></a>Esecuzione di query in colonne crittografate

In questa sezione viene illustrato come eseguire le operazioni seguenti:   
-   Recuperare i valori del testo crittografato archiviati nelle colonne crittografate.   
-   Recuperare i valori del testo non crittografato archiviati nelle colonne crittografate.   
-   Inviare i valori del testo non crittografato destinati alle colonne crittografate (ad esempio, nelle istruzioni `INSERT` o `UPDATE` e come parametri di ricerca delle clausole `WHERE` nelle istruzioni `SELECT`).

### <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>Recupero dei valori del testo crittografato archiviati nelle colonne crittografate    

Per recuperare i valori da una colonna crittografata come testo crittografato (senza decrittografare i valori):
1.  Assicurarsi che Always Encrypted sia disabilitato per la connessione di database per la finestra dell'editor di query da cui si esegue la query `SELECT`. Vedere la sezione [Abilitazione e disabilitazione di Always Encrypted per una connessione di database](#en-dis) più avanti in questo articolo.      
2.  Eseguire una query `SELECT` . I dati recuperati dalle colonne crittografate verranno restituiti come valori binari (crittografati).   

*Esempio*   
Supponendo che `SSN` è una colonna crittografata nella tabella `Patients` , la query riportata di seguito recupererà i valori binari del testo crittografato, se Always Encrypted è disabilitato per la connessione di database.   

![always-encrypted-ciphertext](../../../relational-databases/security/encryption/media/always-encrypted-ciphertext.png)
 
### <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>Recupero dei valori del testo non crittografato archiviati nelle colonne crittografate    

Per recuperare i valori da una colonna crittografata come testo non crittografato (decrittografando i valori):   
1.  Assicurarsi che Always Encrypted sia abilitato per la connessione di database per la finestra dell'editor di query da cui si esegue la query `SELECT`. Ciò indicherà al provider di dati .NET Framework per SQL Server (usato da SSMS) di decrittografare i dati recuperati dalle colonne crittografate. Vedere la sezione [Abilitazione e disabilitazione di Always Encrypted per una connessione di database](#en-dis) più avanti in questo articolo.
2.  Assicurarsi che sia possibile accedere a tutte le chiavi master della colonna configurate per le colonne crittografate. Ad esempio, se la chiave master della colonna è un certificato, è necessario assicurarsi che il certificato venga distribuito nel computer in cui è in esecuzione SSMS. Oppure, se la chiave master della colonna è una chiave archiviata nell'insieme di credenziali delle chiavi di Azure, è necessario assicurarsi di avere le autorizzazioni per accedere alla chiave. Potrebbe inoltre essere richiesto di accedere ad Azure.
3.  Eseguire una query `SELECT` . Tutti i dati recuperati dalle colonne crittografate verranno restituiti come testo non crittografato come valori dei tipi di dati originali.   

*Esempio*   
Supponendo che SSN sia una colonna crittografata `char(11)` nella tabella `Patients` , la query mostrata di seguito restituirà i valori del testo non crittografato se Always Encrypted è abilitato per la connessione di database e se si ha accesso alla chiave master della colonna configurata per la colonna `SSN` .   

![always-encrypted-plaintext](../../../relational-databases/security/encryption/media/always-encrypted-plaintext.png)
 
### <a name="sending-plaintext-values-targeting-encrypted-columns"></a>Invio di valori del testo non crittografato destinati alle colonne crittografate       

Per eseguire una query che invia un valore destinato a una colonna crittografata, ad esempio una query che inserisce, aggiorna o applica un filtro in base a un valore archiviato in una colonna crittografata:

1. Assicurarsi che Always Encrypted sia abilitato per la connessione di database per la finestra dell'editor di query da cui si esegue la query `SELECT`. Ciò indica al provider di dati .NET Framework per SQL Server (usato da SSMS) di crittografare le variabili Transact-SQL con parametri (vedere più avanti) destinate alle colonne crittografate. Vedere la sezione [Abilitazione e disabilitazione di Always Encrypted per una connessione di database](#en-dis) più avanti in questo articolo.
2. Assicurarsi che sia possibile accedere a tutte le chiavi master della colonna configurate per le colonne crittografate. Ad esempio, se la chiave master della colonna è un certificato, è necessario assicurarsi che il certificato venga distribuito nel computer in cui è in esecuzione SSMS. Oppure, se la chiave master della colonna è una chiave archiviata nell'insieme di credenziali delle chiavi di Azure, è necessario assicurarsi di avere le autorizzazioni per accedere alla chiave. Potrebbe inoltre essere richiesto di accedere ad Azure.
3. Assicurarsi che la funzionalità Parametrizzazione per Always Encrypted sia abilitata per la finestra dell'editor di query. Richiede almeno SSMS versione 17.0. Dichiarare una variabile Transact-SQL e inizializzarla con un valore da inviare al database (mediante le operazioni di inserimento, aggiornamento o applicazione del filtro). Per informazioni dettagliate, vedere la sezione [Parametrizzazione per Always Encrypted](#param) più avanti in questo articolo.

   > [!NOTE]
   > Poiché Always Encrypted supporta un subset limitato di conversioni di tipi, in molti casi è necessario che il tipo di dati di una variabile Transact-SQL sia lo stesso tipo della colonna di database di destinazione a cui è destinato.

4. Eseguire la query inviando il valore della variabile Transact-SQL al database. SSMS convertirà la variabile in un parametro di query e crittograferà il relativo valore prima di inviarlo al database.   

*Esempio* Supponendo che `SSN` sia una colonna crittografata `char(11)` nella tabella `Patients`, lo script seguente proverà a trovare una riga contenente `'795-73-9838'` nella colonna SSN e a restituire il valore della colonna `LastName`, a condizione che Always Encrypted sia abilitato per la connessione di database, che la funzionalità Parametrizzazione per Always Encrypted sia abilitata per la finestra dell'editor di query e che si abbia accesso alla chiave master della colonna configurata per la colonna `SSN`.   

![always-encrypted-patients](../../../relational-databases/security/encryption/media/always-encrypted-patients.png)

### <a name="en-dis"></a> Abilitazione e disabilitazione di Always Encrypted per una connessione di database   

Quando si abilita Always Encrypted per una connessione di database, si indica al provider di dati .NET Framework per SQL Server, usato da SQL Server Management Studio, di provare a eseguire le operazioni seguenti in modo trasparente:   
-   Decrittografare tutti i valori recuperati dalle colonne crittografate e restituiti nei risultati della query.   
-   Crittografare i valori delle variabili Transact-SQL con parametri destinati alle colonne di database crittografate.   
Per abilitare Always Encrypted per una connessione di database, specificare `Column Encryption Setting=Enabled` nella scheda **Proprietà aggiuntive** della finestra di dialogo **Connetti al server** .    
Per disabilitare Always Encrypted per una connessione di database, specificare `Column Encryption Setting=Disabled` o rimuovere l'impostazione di **Crittografia di colonna** dalla scheda **Proprietà aggiuntive** della finestra di dialogo **Connetti al server** (il valore predefinito è **Disabilitato**).   

> [!TIP]
> Per abilitare e disabilitare Always Encrypted per una finestra dell'editor di query esistente:   
> 1.    Fare clic con il pulsante destro del mouse in un punto qualsiasi all'interno della finestra dell'editor di query.
> 2.    Selezionare **Connessione** > **Cambia connessione**. 
> 3.    Fare clic su **Opzioni** >>
> 4.    Selezionare la scheda **Proprietà aggiuntive** e digitare `Column Encryption Setting=Enabled` (per abilitare il comportamento di Always Encrypted) o rimuovere l'impostazione (per disabilitare il comportamento di Always Encrypted).   
> 5.    Fare clic su **Connetti**.   
   
### <a name="param"></a>Parametrizzazione per Always Encrypted   
 
Parametrizzazione per Always Encrypted è una funzionalità di SQL Server Management Studio che converte automaticamente le variabili Transact-SQL in parametri di query (istanze della [classe SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)). Richiede almeno SSMS versione 17.0. Ciò consente al provider di dati .NET Framework per SQL Server di rilevare i dati destinati alle colonne crittografate e di crittografare tali dati prima di inviarli al database. 
  
Senza parametrizzazione, il provider di dati .NET Framework passa ogni istruzione creata nell'editor di query come query senza parametri. Se la query contiene valori letterali o variabili Transact-SQL destinate a colonne crittografate, il provider di dati .NET Framework per SQL Server non riuscirà a rilevarle e crittografarle prima di inviare la query al database. Di conseguenza, la query avrà esito negativo a causa di mancata corrispondenza tra i tipi, ovvero tra la variabile Transact-SQL letterale non crittografata e la colonna crittografata. Ad esempio, la query seguente avrà esito negativo senza parametrizzazione, supponendo che la colonna `SSN` sia crittografata.   

```sql
DECLARE @SSN NCHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

#### <a name="enablingdisabling-parameterization-for-always-encrypted"></a>Abilitazione/disabilitazione della funzionalità Parametrizzazione per Always Encrypted

La funzionalità Parametrizzazione per Always Encrypted è disabilitata per impostazione predefinita.

Per abilitare o disabilitare la funzionalità Parametrizzazione per Always Encrypted per la finestra dell'editor di query corrente:

1. Selezionare **Query** dal menu principale.
2. Selezionare **Opzioni query**.
3. Passare a **Esecuzione** > **Avanzata**.
4. Selezionare o deselezionare **Abilita parametrizzazione per Always Encrypted**.
5. Fare clic su **OK**.

Per abilitare/disabilitare la funzionalità Parametrizzazione per Always Encrypted per future finestre dell'editor di query:

1. Selezionare **Strumenti** dal menu principale.
2. Selezionare **Opzioni**.
3. Passare a **Esecuzione query** > **SQL Server** > **Avanzata**.
4. Selezionare o deselezionare **Abilita parametrizzazione per Always Encrypted**.
5. Fare clic su **OK**.

Se si esegue una query in una finestra dell'editor di query che usa una connessione di database con Always Encrypted abilitato, ma la parametrizzazione non è abilitata per la finestra dell'editor di query, verrà richiesto di abilitarla.

> [!NOTE]
> La funzionalità Parametrizzazione per Always Encrypted funziona solo nelle finestre dell'editor di query che usano connessioni di database con l'opzione Always Encrypted abilitata (vedere [Abilitazione e disabilitazione di Always Encrypted per una connessione di database](#en-dis)). Non verrà parametrizzata alcuna variabile Transact-SQL se la finestra dell'editor di query usa una connessione di database senza l'opzione Always Encrypted abilitata.

#### <a name="how-parameterization-for-always-encrypted-works"></a>Funzionamento di Parametrizzazione per Always Encrypted

Se nella connessione di database sono abilitati sia la funzionalità Parametrizzazione per Always Encrypted che il comportamento di Always Encrypted per una finestra dell'editor di query, SQL Server Management Studio proverà a parametrizzare le variabili Transact-SQL che soddisfano le condizioni necessarie seguenti:

- Le variabili devono essere dichiarate e inizializzate nella stessa istruzione (inizializzazione inline). Le variabili dichiarate con istruzioni `SET` separate non verranno parametrizzate.
- Le variabili devono essere inizializzate con un singolo valore letterale. Le variabili inizializzate con espressioni che comprendono operatori o funzioni non verranno parametrizzate.

Di seguito sono riportati alcuni esempi di variabili che verranno parametrizzate da SQL Server Management Studio.

```sql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

Di seguito sono riportati invece alcuni esempi di variabili che non verranno parametrizzate da SQL Server Management Studio:

```sql
DECLARE @Name nvarchar(50); --Initialization seperate from declaration
SET @Name = 'Abel';

DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal

DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
Per far sì che la parametrizzazione riesca:   
- Il tipo del valore letterale usato per l'inizializzazione della variabile da parametrizzare deve corrispondere al tipo nella dichiarazione di variabile.   
- Se il tipo dichiarato della variabile è un tipo data o ora, la variabile deve essere inizializzata usando una stringa con uno dei formati conformi a ISO 8601 seguenti.   

Di seguito sono riportati alcuni esempi di dichiarazioni di variabili Transact-SQL che causano errori di parametrizzazione:   
```sql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```
SQL Server Management Studio usa Intellisense per indicare le variabili che possono essere parametrizzate correttamente e quelle la cui parametrizzazione non riuscirà e il motivo.   

Una dichiarazione di una variabile che può essere parametrizzata correttamente è contrassegnata con una sottolineatura di avviso nell'editor di query. Se si passa il mouse su un'istruzione di dichiarazione contrassegnata con una sottolineatura di avviso, verranno visualizzati i risultati del processo di parametrizzazione, inclusi i valori delle proprietà chiave dell'oggetto [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) risultante (la variabile a cui viene eseguito il mapping): [SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx), [Size](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.size.aspx), [Precision](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.precision.aspx), [Scale](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.scale.aspx), [SqlValue](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqlvalue.aspx). È anche possibile visualizzare l'elenco completo di tutte le variabili che sono state parametrizzate correttamente nella scheda **Avviso** della vista **Elenco errori** . Per aprire la vista **Elenco errori** , selezionare **Vista** dal menu principale, quindi selezionare **Elenco errori**.    

Se SQL Server Management Studio ha provato a parametrizzare una variabile, ma la parametrizzazione non è riuscita, la dichiarazione della variabile verrà contrassegnata con una sottolineatura di errore. Se si passa il mouse sull'istruzione di dichiarazione contrassegnata con una sottolineatura di errore, verranno visualizzati i risultati relativi all'errore. È anche possibile visualizzare l'elenco completo degli errori di parametrizzazione per tutte le variabili nella scheda **Errore** della vista **Elenco errori** . Per aprire la vista **Elenco errori** , selezionare **Vista** dal menu principale, quindi selezionare **Elenco errori**.   

La schermata seguente mostra un esempio di sei dichiarazioni di variabili. SQL Server Management Studio ha parametrizzato correttamente le prime tre variabili. Le ultime tre variabili non hanno soddisfatto le condizioni necessarie per la parametrizzazione e pertanto SQL Server Management Studio non ha provato a parametrizzarle (le relative dichiarazioni non vengono contrassegnate in alcun modo).

![always-encrypted-parameter-warnings](../../../relational-databases/security/encryption/media/always-encrypted-parameter-warnings.png)
 
Un altro esempio riportato di seguito mostra due variabili che soddisfano le condizioni necessarie per la parametrizzazione, ma il tentativo di parametrizzazione non è riuscito perché le variabili sono state inizializzate in modo non corretto.    
 
![always-encrypted-error](../../../relational-databases/security/encryption/media/always-encrypted-error.png)
 
> [!NOTE]
> Poiché Always Encrypted supporta un subset limitato di conversioni di tipi, in molti casi è necessario che il tipo di dati di una variabile Transact-SQL sia lo stesso tipo della colonna di database di destinazione a cui è destinato. Ad esempio, supponendo che il tipo della colonna `SSN` nella tabella `Patients` è `char(11)`, la query sottostante avrà esito negativo perché il tipo della variabile `@SSN` , ovvero `nchar(11)`, non corrisponde al tipo della colonna.   

```sql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

    Msg 402, Level 16, State 2, Line 5   
    The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
    and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator.

> [!NOTE]
> Senza la parametrizzazione, l'intera query, incluse le conversioni dei tipi, viene elaborata all'interno di SQL Server o del database SQL di Azure. Con parametrizzazione abilitata, alcune conversioni dei tipi vengono eseguite da .NET Framework all'interno di SQL Server Management Studio. A causa delle differenze tra il sistema dei tipi .NET Framework e il sistema dei tipi SQL Server (ad esempio diversa precisione di alcuni tipi come float), una query eseguita con la parametrizzazione abilitata può produrre risultati diversi rispetto alla query eseguita senza la parametrizzazione abilitata. 

#### <a name="permissions-for-querying-against-encrypted-columns"></a>Autorizzazioni per l'esecuzione di query su colonne crittografate

Per eseguire le query su colonne crittografate, incluse le query che recuperano i dati in testo crittografato, sono necessarie le autorizzazioni `VIEW ANY COLUMN MASTER KEY DEFINITION` e `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` nel database.

Oltre a queste autorizzazioni, per decrittografare i risultati delle query o per crittografare i parametri di query (generati dalla parametrizzazione delle variabili Transact-SQL), è necessario anche accedere alla chiave master della colonna proteggendo le colonne di destinazione:

- **Archivio certificati - Computer locale**: è necessario avere l'accesso `Read` al certificato usato come chiave master della colonna o essere l'amministratore del computer.   
- **Insieme di credenziali delle chiavi di Azure** : sono necessarie le autorizzazioni `get`, `unwrapKey`e verify per l'insieme di credenziali contenente la chiave master della colonna.
- **Provider dell'archivio chiavi (KSP)** : l'autorizzazione e le credenziali necessarie quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione KSP.   
- **Provider del servizio di crittografia (CSP)** : l'autorizzazione e le credenziali richieste quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione CSP.

Per altre informazioni, vedere [Creare e archiviare chiavi master della colonna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

<a name="provisioncmk"></a>
## <a name="provisioning-column-master-keys-new-column-master-key"></a>Provisioning di chiavi master della colonna (Nuova chiave master della colonna)

La finestra di dialogo **Nuova chiave master della colonna** consente di generare una chiave master della colonna o selezionare una chiave esistente in un archivio chiavi e di creare i metadati della chiave master della colonna per la chiave selezionata o creata nel database.

1.  In **Esplora oggetti** passare alla cartella **Sicurezza > Chiavi con crittografia sempre attiva** del database.
2.  Fare clic con il pulsante destro del mouse sulla cartella **Chiavi master della colonna** e selezionare **Nuova chiave master della colonna**. 
3.  Nella finestra di dialogo **Nuova chiave master della colonna** immettere il nome dell'oggetto metadati della chiave master della colonna.
4.  Selezionare un archivio chiavi:
    - **Archivio certificati - Utente corrente**: indica il percorso dell'archivio certificati Utente corrente nell'archivio certificati di Windows, ovvero nell'archivio personale. 
    - **Archivio certificati - Computer locale**: indica il percorso dell'archivio certificati Computer locale nell'archivio certificati di Windows. 
    - **Azure Key Vault**: è necessario accedere ad Azure facendo clic su **Accedi**. Eseguito l'accesso, sarà possibile selezionare uno degli abbonamenti di Azure e un insieme di credenziali delle chiavi.
    - **Provider dell'archivio chiavi (KSP)** : indica un archivio chiavi che è accessibile tramite un provider dell'archivio chiavi (KSP) che implementa l'API CNG (Cryptography Next Generation). In genere, questo tipo di archivio è un modulo di protezione hardware (HSM). Dopo aver selezionato questa opzione, è necessario selezionare un provider dell'archivio chiavi. Viene selezionato per impostazione predefinita il**provider dell'archivio chiavi del software Microsoft** . Per usare una chiave master della colonna archiviata in un HSM, selezionare un provider dell'archivio chiavi per il dispositivo, che deve essere installato e configurato nel computer prima di aprire la finestra di dialogo.
    -   **Provider del servizio di crittografia (CSP)** : un archivio chiavi accessibile attraverso un provider del servizio di crittografia (CSP) che implementa l'API di crittografia (CAPI). In genere, questo archivio è un modulo di protezione hardware (HSM). Dopo aver selezionato questa opzione, è necessario selezionare un provider del servizio di crittografia.  Per usare una chiave master della colonna archiviata in un HSM, selezionare un provider del servizio di crittografia per il dispositivo, che deve essere installato e configurato nel computer prima di aprire la finestra di dialogo.
    
    > [!NOTE]
    > Poiché CAPI è un'API deprecata, il provider del servizio di crittografia è disabilitato per impostazione predefinita. È possibile abilitarlo creando il valore DWORD CAPI Provider Enabled sotto la chiave **[HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\sql13\Tools\Client\Always Encrypted]** nel Registro di sistema di Windows e impostando il valore su 1. È consigliabile usare CNG anziché CAPI, a meno che l'archivio chiavi non supporti CNG.
   
    Per altre informazioni sugli archivi chiavi indicati sopra, vedere [Creare e archiviare chiavi master della colonna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

5.  Selezionare una chiave esistente nell'archivio chiavi oppure fare clic sul pulsante **Genera chiave** o **Genera certificato** per creare una chiave nell'archivio chiavi. 
6.  Fare clic su **OK** e la nuova chiave verrà visualizzata nell'elenco. 

SQL Server Management Studio crea i metadati per la chiave master della colonna nel database. Nella finestra di dialogo viene generata e rilasciata un'istruzione [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) .


<a name="provisioncek"></a> 
## <a name="provisioning-column-encryption-keys-new-column-encryption-key"></a>Provisioning delle chiavi di crittografia della colonna (Nuova chiave di crittografia della colonna)

La finestra di dialogo **Nuova chiave di crittografia della colonna** consente di generare una chiave di crittografia della colonna, crittografarla con una chiave master della colonna e creare i metadati della chiave di crittografia della colonna nel database.

1.  In **Esplora oggetti**passare alla cartella **Sicurezza/Chiavi con crittografia sempre attiva** del database.
2.  Fare clic con il pulsante destro del mouse sulla cartella **Chiavi di crittografia della colonna** e selezionare **Nuova chiave di crittografia della colonna**. 
3.  Nella finestra di dialogo **Nuova chiave di crittografia della colonna** immettere il nome dell'oggetto metadati della chiave di crittografia della colonna.
4.  Selezionare un oggetto metadati che rappresenta la chiave master della colonna nel database.
5.  Fare clic su **OK**. 


SQL Server Management Studio genera una nuova chiave di crittografia della colonna e consente di recuperare i metadati per la chiave master della colonna selezionata dal database. SQL Server Management Studio userà quindi i metadati della chiave master della colonna per contattare l'archivio chiavi contenente la chiave master della colonna e crittografare la chiave di crittografia della colonna. Infine, vengono creati nel database i metadati per la nuova chiave di crittografia della colonna. Nella finestra di dialogo viene generata e rilasciata un'istruzione [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) .

### <a name="permissions-for-provisioning-a-column-encryption-key"></a>Autorizzazioni per il provisioning di una chiave di crittografia della colonna

Sono necessarie le autorizzazioni *ALTER ANY ENCRYPTION MASTER KEY* e *VIEW ANY COLUMN MASTER KEY DEFINITION* del database per creare nella finestra di dialogo i metadati della chiave di crittografia della colonna e accedere ai metadati della chiave master della colonna.
Per accedere a un archivio chiavi e usare la chiave master della colonna, è possibile richiedere le autorizzazioni per l'archivio chiavi e/o la chiave:
- **Archivio certificati - Computer locale**: è necessario avere accesso in lettura al certificato usato come chiave master della colonna o essere l'amministratore del computer.
- **Azure Key Vault**: sono necessarie le autorizzazioni *get*, *unwrapKey*, *wrapKey*, *sign* e *verify* per l'insieme di credenziali contenente la chiave master della colonna.
- **Provider dell'archivio chiavi (CNG)** : l'autorizzazione e le credenziali obbligatorie potrebbero essere richieste quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione KSP.
- **Provider del servizio di crittografia (CAPI)** : potrebbero essere richieste l'autorizzazione e le credenziali obbligatorie quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione CSP.

Per altre informazioni, vedere [Creare e archiviare chiavi master della colonna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

<a name="rotatecmk"></a>
## <a name="rotating-column-master-keys"></a>Rotazione delle chiavi master di colonna

La rotazione di una chiave master della colonna è il processo di sostituzione di una chiave master della colonna esistente con la nuova chiave. Potrebbe essere necessario ruotare una chiave se questa è stata compromessa oppure per conformità ai criteri e alle normative dell'organizzazione che impongono la rotazione a intervalli regolari delle chiavi crittografiche. La rotazione delle chiavi master della colonna interessa la decrittografia delle chiavi di crittografia della colonna che sono protette dalla chiave master corrente della colonna, la loro successiva crittografia tramite la chiave master nuova della colonna e l'aggiornamento dei metadati per entrambi i tipi di chiavi. Per altre informazioni, vedere [Panoramica della gestione delle chiavi per Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

**Passaggio 1: Eseguire il provisioning di una nuova chiave master della colonna**

Effettuare il provisioning di una nuova chiave master della colonna seguendo la procedura descritta nella sezione Provisioning delle chiavi master della colonna.

**Passaggio 2: Eseguire la crittografia delle chiavi di crittografia della colonna con la nuova chiave master della colonna**

Una chiave master della colonna protegge in genere uno o più chiavi di crittografia di colonna. Una chiave master della colonna protegge in genere una o più chiavi di crittografia della colonna. Ognuna di queste chiavi contiene un valore crittografato e archiviato nel database, che è il risultato della crittografia della chiave di crittografia con la chiave master della colonna.
In questo passaggio è necessario crittografare tutte le chiavi di crittografia della colonna protette con la chiave master della colonna, eseguendo la rotazione con la nuova chiave master della colonna e archiviando il nuovo valore crittografato nel database. Di conseguenza, ogni chiave di crittografia della colonna interessata dalla rotazione avrà due valori crittografati: un valore crittografato con la chiave master della colonna esistente e un nuovo valore crittografato con la nuova chiave master della colonna.

1.  In **Esplora oggetti** passare alla cartella **Sicurezza>Chiavi Always Encrypted>Chiavi master della colonna** e individuare la chiave master della colonna per la rotazione.
2.  Fare clic con il pulsante destro del mouse sulla chiave master della colonna e selezionare **Ruota**.
3.  Nella finestra **Rotazione della chiave master della colonna** selezionare il nome della nuova chiave master della colonna creata nel passaggio 1 nel campo **Destinazione** .
4.  Consultare l'elenco delle chiavi di crittografia della colonna protette dalle chiavi master della colonna esistenti. Queste chiavi saranno coinvolte nella rotazione.
5.  Fare clic su **OK**.

SQL Server Management Studio ottiene i metadati delle chiavi di crittografia della colonna protette con la chiave master della colonna precedente e i metadati delle chiavi master della colonna vecchie e nuove. Quindi, SSMS usa i metadati della chiave master della colonna per accedere all'archivio dati contenente la chiave master della colonna precedente e decrittografare le chiavi di crittografia della colonna. Successivamente, SSMS accede all'archivio chiavi contenente la nuova chiave master della colonna per produrre un nuovo set di valori crittografati delle chiavi di crittografia della colonna e quindi aggiunge i nuovi valori ai metadati generando ed emettendo istruzioni [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) .

> [!NOTE]
> Verificare che ogni chiave di crittografia della colonna, crittografata con la chiave master della colonna precedente, non sia crittografata con altre chiavi master della colonna. In altre parole, ogni chiave di crittografia della colonna interessata dalla rotazione deve avere un solo valore crittografato nel database. Se una chiave di crittografia della colonna interessata contiene più di un valore crittografato, è necessario rimuovere il valore prima di procedere con la rotazione (vedere il *passaggio 4* per la rimozione di un valore crittografato da una chiave di crittografia della colonna).

**Passaggio 3: Configurare le applicazioni con la nuova chiave master della colonna**

In questo passaggio è necessario verificare che tutte le applicazioni client in uso che eseguono query nelle colonne del database protette dalla chiave master della colonna in fase di rotazione siano in grado di accedere alla nuova chiave master della colonna, ad esempio le colonne del database crittografate con una chiave di crittografia della colonna crittografata con la chiave master della colonna. Questo passaggio dipende dal tipo di archivio chiavi in cui si trova la nuova chiave master della colonna. Esempio:

- Se la nuova chiave master della colonna è un certificato archiviato nell'archivio certificati di Windows, è necessario distribuire il certificato nella posizione dell'archivio dei certificati (*Utente corrente* o *Computer locale*) e nella posizione specificata nel percorso della chiave master della colonna nel database. L'applicazione deve poter accedere al certificato:
  - Se il certificato viene archiviato nel percorso dell'archivio certificati *Utente corrente*, deve essere importato nell'archivio Utente corrente dell'identità Windows dell'applicazione (utente).
  - Se il certificato viene archiviato nel percorso dell'archivio certificati *Computer locale*, l'identità Windows dell'applicazione deve disporre dell'autorizzazione per accedere al certificato.
- Se la nuova chiave master della colonna viene archiviata nell'insieme di credenziali delle chiavi di Microsoft Azure, deve essere implementata per l'autenticazione in Azure e deve essere autorizzata ad accedere alla chiave.

Per i dettagli,vedere [Creare e archiviare chiavi master della colonna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

> [!NOTE]
> A questo punto della rotazione, sia la nuova chiave master della colonna che quella precedente sono valide e possono essere usate per accedere ai dati.

**Passaggio 4: Eseguire la pulizia dei valori della chiave di crittografia della colonna crittografati con la chiave master della colonna precedente**

Dopo aver configurato tutte le applicazioni per l'uso con la nuova chiave master della colonna, rimuovere dal database i valori delle chiavi di crittografia della colonna, crittografate con la chiave master della colonna *precedente* . La rimozione dei valori precedenti predispone il sistema per la rotazione successiva. Tenere presente che ogni chiave di crittografia della colonna, protetta con una chiave master della colonna da ruotare, deve avere esattamente un valore crittografato.

Un altro motivo per cui è necessario pulire il valore precedente prima di archiviare o rimuovere la chiave master della colonna precedente riguarda le prestazioni: quando si eseguono query su una colonna crittografata, un driver client abilitato per la crittografia sempre attiva potrebbe tentare di decrittografare due valori, il valore precedente e quello nuovo. Il driver non riconosce quale delle due chiavi master della colonna sia valida nell'ambiente dell'applicazione, quindi recupera entrambi i valori dal server. Se la decrittografia di uno dei valori non va a buon fine in ragione del fatto che il valore è protetto con una chiave master della colonna non disponibile (ad esempio, la chiave master della colonna precedente rimossa dall'archivio), il driver tenterà di decrittografare un altro valore usando la nuova chiave master della colonna.

> [!WARNING]
> Se si rimuove il valore di una chiave di crittografia della colonna prima che la relativa chiave master della colonna diventi disponibile per un'applicazione, l'applicazione non sarà più in grado di decrittografare la colonna del database.

1.  In **Esplora oggetti** passare alla cartella **Sicurezza>Chiavi con crittografia sempre attiva** e individuare la chiave master della colonna esistente da sostituire.
2.  Fare clic con il pulsante destro del mouse sulla chiave master della colonna esistente e selezionare **Pulizia**.
3.  Verificare l'elenco dei valori delle chiavi di crittografia della colonna da rimuovere.
4.  Fare clic su **OK**.

SQL Server Management Studio rilascerà istruzioni [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) per eliminare i valori crittografati delle chiavi di crittografia della colonna crittografati con la chiave master della colonna precedente.

**Passaggio 5: Eliminare i metadati per la chiave master della colonna precedente**

Se si sceglie di rimuovere la definizione della chiave master della colonna precedente dal database, eseguire la procedura descritta di seguito.

1. In **Esplora oggetti** passare alla cartella **Sicurezza>Chiavi con crittografia sempre attiva>Chiavi master della colonna** e individuare la chiave master della colonna precedente da rimuovere dal database.
2. Fare clic con il pulsante destro del mouse sulla chiave master della colonna precedente e selezionare **Elimina**. In questo modo viene generata e rilasciata un'istruzione [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md) per rimuovere i metadati della colonna chiave master.
3. Fare clic su **OK**.

> [!NOTE]
> Si consiglia di non eliminare definitivamente la chiave master della colonna precedente dopo la rotazione. È opportuno invece mantenere la chiave master della colonna precedente nell'archivio chiavi in cui si trova o archiviarla in un altro posto sicuro. Se si ripristina il database da un file di backup creato prima della configurazione della nuova chiave master della colonna, sarà necessaria la chiave precedente per accedere ai dati.

### <a name="permissions-for-rotating-column-master-key"></a>Autorizzazioni per la rotazione della chiave master della colonna

La rotazione di una chiave master della colonna richiede le seguenti autorizzazioni di database:

- **ALTER ANY COLUMN MASTER KEY**: richiesta per creare i metadati per la nuova chiave master della colonna ed eliminare i metadati per la chiave master della colonna precedente.
- **ALTER ANY COLUMN ENCRYPTION KEY**: richiesta per modificare i metadati della chiave di crittografia della colonna (aggiunta di nuovi valori crittografati).
- **VIEW ANY COLUMN MASTER KEY DEFINITION** : richiesta per accedere e leggere i metadati delle chiavi master della colonna.
- **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** : richiesta per accedere e leggere i metadati delle chiavi di crittografia della colonna. 

È necessario essere in grado di accedere sia alla chiave master della colonna precedente, sia alla nuova chiave master della colonna nei rispettivi archivi chiavi. Per accedere a un archivio chiavi e usare una chiave master della colonna, è possibile richiedere le autorizzazioni per l'archivio chiavi e/o la chiave:
- **Archivio certificati - Computer locale**: è necessario avere accesso in lettura al certificato usato come chiave master della colonna o essere l'amministratore del computer.
- **Azure Key Vault**: sono necessarie le autorizzazioni *create*, *get*, *unwrapKey*, *wrapKey*, *sign*e *verify* per l'insieme di credenziali contenente le chiavi master della colonna.
- **Provider dell'archivio chiavi (CNG)** : l'autorizzazione e le credenziali obbligatorie potrebbero essere richieste quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione KSP.
- **Provider del servizio di crittografia (CAPI)** : potrebbero essere richieste l'autorizzazione e le credenziali obbligatorie quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione CSP.

Per altre informazioni, vedere [Creare e archiviare chiavi master della colonna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

<a name="rotatecek"></a> 
## <a name="rotating-column-encryption-keys"></a>Rotazione delle chiavi di crittografia della colonna

La rotazione di una chiave di crittografia della colonna comporta la decrittografia dei dati in tutte le colonne crittografate con la chiave da ruotare e la nuova crittografia dei dati che usano la nuova chiave di crittografia della colonna.

>[!NOTE]
> La rotazione di una chiave di crittografia della colonna può richiedere molto tempo, se le tabelle contenenti le colonne crittografate con la chiave da ruotare sono di grandi dimensioni. Durante la nuova crittografia dei dati, le applicazioni non possono scrivere nelle tabelle interessate. Pertanto, l'organizzazione deve pianificare con molta attenzione una rotazione della chiave di crittografia della colonna.
Per ruotare una chiave di crittografia della colonna, usare la procedura guidata di Always Encrypted.

1.  Aprire la procedura guidata per il database: fare clic con il pulsante destro del mouse sul database, scegliere **Attività**, quindi fare clic su **Crittografa colonne**.
2.  Leggere la pagina **Introduzione** , quindi fare clic su **Avanti**.
3.  Nella pagina **Selezione colonne** espandere le tabelle e individuare tutte le colonne da sostituire che attualmente vengono crittografate con la chiave di crittografia della colonna precedente.
4.  Per ogni colonna crittografata con la chiave di crittografia precedente, impostare **Chiave di crittografia** su una nuova chiave generata automaticamente. **Nota:** in alternativa è possibile creare una nuova chiave di crittografia della colonna prima di eseguire la procedura guidata. Vedere la sezione *Provisioning delle chiavi di crittografia della colonna*.
5.  Nella pagina **Configurazione chiave master** , selezionare un percorso per archiviare la nuova chiave, selezionare un'origine della chiave master e quindi fare clic su **Avanti**. **Nota:** se si usa una chiave di crittografia della colonna già esistente (non una generata automaticamente), non deve essere eseguita alcuna azione in questa pagina.
6.  Nella pagina **Convalida**scegliere se eseguire lo script immediatamente o creare uno script di PowerShell, quindi fare clic su **Avanti**.
7.  Nella pagina **Riepilogo** esaminare le opzioni selezionate, quindi fare clic su **Fine** e chiudere la procedura guidata quando viene completata.
8.  In **Esplora oggetti**passare alla cartella **Sicurezza/Chiavi con crittografia sempre attiva/Chiavi di crittografia della colonna** e individuare la chiave di crittografia della colonna precedente da rimuovere dal database. Fare clic sulla chiave con il pulsante destro del mouse e selezionare **Elimina**.

### <a name="permissions-for-rotating-column-encryption-keys"></a>Autorizzazioni per la rotazione delle chiavi di crittografia della colonna

La rotazione di una chiave master della colonna richiede le autorizzazioni di database seguenti: **ALTER ANY COLUMN MASTER KEY**: richiesta se si usa una nuova chiave di crittografia della colonna generata automaticamente. Verranno generati anche una nuova chiave master della colonna e i relativi metadati.
**ALTER ANY COLUMN ENCRYPTION KEY**: richiesta per aggiungere metadati per la nuova chiave di crittografia della colonna.
**VIEW ANY COLUMN MASTER KEY DEFINITION** : richiesta per accedere e leggere i metadati delle chiavi master della colonna.
**VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** : richiesta per accedere e leggere i metadati delle chiavi di crittografia della colonna.

È necessario essere in grado di accedere alle chiavi master sia per la nuova chiave di crittografia della colonna, sia per la chiave di crittografia precedente. Per accedere a un archivio chiavi e usare una chiave master della colonna, è possibile richiedere le autorizzazioni per l'archivio chiavi e/o la chiave:
- **Archivio certificati - Computer locale**: è necessario avere accesso in lettura al certificato usato come chiave master della colonna o essere l'amministratore del computer.
- **Azure Key Vault**: sono necessarie le autorizzazioni get, unwrapKey e verify per l'insieme di credenziali contenente la chiave master della colonna.
- **Provider dell'archivio chiavi (CNG)** : l'autorizzazione e le credenziali obbligatorie potrebbero essere richieste quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione KSP.
- **Provider del servizio di crittografia (CAPI)** : potrebbero essere richieste l'autorizzazione e le credenziali obbligatorie quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione CSP.

Per altre informazioni, vedere [Creare e archiviare chiavi master della colonna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

## <a name="performing-dac-upgrade-operations-when-database-or-dacpac-uses-always-encrypted"></a>Esecuzione di operazioni di aggiornamento dell'applicazione livello dati quando il database o il file DACPAC usa Always Encrypted

Le[operazioni dell'applicazione livello dati](../../data-tier-applications/data-tier-applications.md) sono supportati nei file DACPAC e nei database con schemi che contengono colonne crittografate. L'operazione di aggiornamento dell'applicazione livello dati richiede una particolare attenzione: vedere la procedura [Aggiornare un'applicazione livello dati](../../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md) per le modalità di esecuzione di un aggiornamento dell'applicazione livello dati in vari strumenti, tra cui SSMS. 

Quando si aggiorna un database usando un file DACPAC e il file DACPAC o il database di destinazione contiene colonne crittografate, l'operazione di aggiornamento attiva un'operazione di crittografia dei dati se vengono soddisfatte tutte le condizioni seguenti:
- Il database contiene una colonna con dati.
- La stessa colonna esiste nel file DACPAC.
- La configurazione di crittografia della colonna nel database è diversa dalla configurazione della colonna corrispondente nel file DACPAC. Vedere la tabella seguente per i dettagli.

| Condizione|Azione|
|:---|:---|
|La colonna è crittografata nel file DACPAC e non è crittografata nel database.| I dati contenuti nella colonna verranno crittografati.|
|La colonna non è crittografata nel file DACPAC ed è crittografata nel database.| I dati presenti nella colonna verranno decrittografati ovvero la crittografia verrà rimossa dalla colonna.|
| La colonna è crittografata sia nel file DACPAC che nel database, ma la colonna nel file DACPAC usa un tipo diverso di crittografia e/o una chiave di crittografia della colonna diversa rispetto alla colonna corrispondente nel database.|I dati presenti nella colonna verranno decrittografati e di nuovo crittografati in modo da corrispondere alla configurazione di crittografia nel file DACPAC.|

> [!NOTE]
> Se la chiave master della colonna configurata per la colonna nel database o nel file DACPAC viene archiviata nell'insieme di credenziali delle chiavi di Azure, verrà richiesto di accedere ad Azure, a meno che l'accesso non sia già stato eseguito.

### <a name="permissions-for-dac-upgrade-if-always-encrypted-is-set-up"></a>Autorizzazioni per l'aggiornamento dell'applicazione livello dati se Always Encrypted è configurato

Per eseguire un'operazione di aggiornamento dell'applicazione livello dati se Always Encrypted è configurato nel file DACPAC o nel database di destinazione, potrebbero essere necessarie alcune o tutte le autorizzazioni indicate di seguito, in base alle differenze tra lo schema nel file DACPAC e lo schema del database di destinazione.

*ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*, *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION*

Se l'operazione di aggiornamento attiva un'operazione di crittografia dei dati, è necessario essere in grado di accedere alle chiavi master della colonna configurate per le colonne interessate:

- **Archivio certificati - Computer locale**: è necessario avere accesso in lettura al certificato usato come chiave master della colonna o essere l'amministratore del computer.
- **Azure Key Vault**: sono necessarie le autorizzazioni *create*, *get*, *unwrapKey*, *wrapKey*, *sign*e *verify* per l'insieme di credenziali contenente la chiave master della colonna.
- **Provider dell'archivio chiavi (CNG)** : l'autorizzazione e le credenziali obbligatorie potrebbero essere richieste quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione KSP.
- **Provider del servizio di crittografia (CAPI)** : potrebbero essere richieste l'autorizzazione e le credenziali obbligatorie quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione CSP.

Per altre informazioni, vedere [Creare e archiviare chiavi master della colonna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

## <a name="migrating-databases-with-encrypted-columns-using-bacpac"></a>Migrazione di database con colonne crittografate con un file BACPAC

Quando si esporta un database, tutti i dati archiviati nelle colonne crittografate vengono recuperati e inseriti nel file [BACPAC](../../data-tier-applications/data-tier-applications.md) risultante (in formato crittografato). Il file BACPAC risultante contiene anche i metadati per le chiavi di Always Encrypted.

Quando si importa il file BACPAC in un database, i dati crittografati del file BACPAC vengono caricati nel database e i metadati delle chiavi di Always Encrypted vengono ricreati.

Se si usa un'applicazione configurata per modificare o recuperare i dati crittografati archiviati nel database di origine (quello esportato), non sono necessarie operazioni particolari per consentire all'applicazione di eseguire query sui dati crittografati nel database di destinazione, perché le chiavi presenti in entrambi i database sono le stesse.

### <a name="permissions-for-migrating-databases-with-encrypted-columns"></a>Autorizzazioni per la migrazione di database con colonne crittografate

Sono necessarie le autorizzazioni *ALTER ANY COLUMN MASTER KEY* e *ALTER ANY COLUMN ENCRYPTION KEY* per il database di origine. Per il database di destinazione sono necessarie le autorizzazioni *ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*e *VIEW ANY COLUMN ENCRYPTION* .

## <a name="migrating-databases-with-encrypted-columns-using-sql-server-import-and-export-wizard"></a>Migrazione di database con colonne crittografate usando l'importazione e l'esportazione guidate di SQL Server

Rispetto all'uso dei file BACPAC, la [procedura guidata di importazione ed esportazione di SQL Server](~/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md) offre maggiore controllo sulla modalità di gestione dei dati archiviati nelle colonne crittografate durante la migrazione dei dati.

- Se l'origine dati è un database che usa Always Encrypted, è possibile configurare la connessione dell'origine dati in modo che i dati archiviati nelle colonne crittografate vengano decrittografati durante l'operazione di esportazione o rimangano crittografati.
- Se la destinazione dei dati è un database che usa Always Encrypted, è possibile configurare la connessione della destinazione dei dati in modo che i dati destinati alle colonne crittografate vengano crittografati.

Per abilitare la decrittografia (per l'origine dati) o la crittografia (per la destinazione dei dati), è necessario configurare la connessione dell'origine/destinazione dei dati per usare il [provider di dati .Net Framework per SqlServer](https://msdn.microsoft.com/library/system.data.sqlclient.aspx) ed è necessario impostare le parole chiave della stringa di connessione dell'impostazione di crittografia di colonna su *Abilitata*.

Nella tabella seguente sono riportati gli scenari di migrazione possibili con le modalità di interazione con Always Encrypted e la configurazione di origine e destinazione dei dati per ogni connessione.

| Scenario|Configurazione della connessione di origine| Configurazione della connessione di destinazione
|:---|:---|:---
|Crittografare i dati sulla migrazione; i dati vengono archiviati come testo non crittografato nell'origine dati e viene eseguita la migrazione nelle colonne crittografate nella destinazione dei dati.| Provider di dati/driver: *qualsiasi*<br><br>Impostazione di crittografia di colonna = Disabilitata<br><br>(se si usano il provider di dati .net Framework per SqlServer e .NET Framework 4.6 o versione successiva) | (se si usano il provider di dati *.net Framework per SqlServer* e .NET Framework 4.6 o versione successiva)<br><br>Impostazione di crittografia di colonna = Abilitata
| Decrittografare i dati sulla migrazione. I dati vengono archiviati nelle colonne crittografate dell'origine dati e viene eseguita la migrazione in testo non crittografato nella destinazione dei dati. Se la destinazione dei dati è un database, le colonne di destinazione non vengono crittografate.<br><br>**Nota:** le tabelle di destinazione con colonne crittografate devono esistere prima della migrazione.|(se si usano il provider di dati *.net Framework per SqlServer* e .NET Framework 4.6 o versione successiva)<br><br>Column Encryption Setting=Enabled|Provider di dati/driver: *qualsiasi*<br><br>Impostazione di crittografia di colonna = Disabilitata<br><br>(se si usano il provider di dati .net Framework per SqlServer e .NET Framework 4.6 o versione successiva)
|Crittografare nuovamente i dati sulla migrazione; i dati vengono archiviati nelle colonne crittografate dell'origine dati e viene eseguita la migrazione in testo non crittografato nelle colonne della destinazione dei dati che usano tipi di crittografia diversi per le chiavi di crittografia della colonna.<br><br>**Nota:** le tabelle di destinazione con colonne crittografate devono esistere prima della migrazione.| (se si usano il provider di dati *.net Framework per SqlServer* e .NET Framework 4.6 o versione successiva)<br><br>Column Encryption Setting=Enabled|(se si usano il provider di dati *.net Framework per SqlServer* e .NET Framework 4.6 o versione successiva)<br><br>Column Encryption Setting=Enabled
|Spostare i dati crittografati senza decrittografarli.<br><br>**Nota:** le tabelle di destinazione con colonne crittografate devono esistere prima della migrazione.| Provider di dati/driver: *qualsiasi*<br>Impostazione di crittografia di colonna = Disabilitata<br><br>(se si usano il provider di dati .net Framework per SqlServer e .NET Framework 4.6 o versione successiva)| Provider di dati/driver: *qualsiasi*<br>Impostazione di crittografia di colonna = Disabilitata<br><br>(se si usano il provider di dati .net Framework per SqlServer e .NET Framework 4.6 o versione successiva)<br><br>L'utente deve avere impostato ALLOW_ENCRYPTED_VALUE_MODIFICATIONS su ON.<br><br>Per i dettagli, vedere [Migrare dati sensibili protetti da Crittografia sempre attiva](../../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).

### <a name="permissions-for-database-migration-using-sql-server-import-and-export-wizard"></a>Autorizzazioni per la migrazione di database usando l'importazione e l'esportazione guidate di SQL Server

Per **crittografare** o **decrittografare** i dati memorizzati nell'origine dati, sono necessarie le autorizzazioni *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* nel database di origine.

È anche necessario accedere alle chiavi master della colonna, configurate per le colonne, in cui sono archiviati i dati da crittografare o decrittografare:

- **Archivio certificati - Computer locale**: è necessario avere accesso in lettura al certificato usato come chiave master della colonna o essere l'amministratore del computer.
- **Azure Key Vault**: sono necessarie le autorizzazioni get, unwrapKey, wrapKey, sign e verify per l'insieme di credenziali contenente la chiave master della colonna.
- **Provider dell'archivio chiavi (CNG)** : l'autorizzazione e le credenziali necessarie quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione KSP.
- **Provider del servizio di crittografia (CAPI)** : l'autorizzazione e le credenziali richieste quando si usa un archivio chiavi o una chiave, in base all'archivio e alla configurazione CSP.
Per altre informazioni, vedere [Creare e archiviare chiavi master della colonna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

## <a name="see-also"></a>Vedere anche
- [Always Encrypted (Motore di database)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Procedura guidata Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md)
- [Panoramica della gestione delle chiavi per Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Creare e archiviare chiavi master della colonna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [Always Encrypted (sviluppo client)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
- [Configurare Always Encrypted tramite PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)