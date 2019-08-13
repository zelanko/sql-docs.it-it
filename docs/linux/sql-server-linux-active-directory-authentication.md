---
title: "Esercitazione: Usare l'autenticazione di Active Directory per SQL Server in Linux"
titleSuffix: SQL Server
description: Questa esercitazione illustra le procedure di configurazione dell'autenticazione di Active Directory per SQL Server in Linux.
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 69bbeb31f8da4023bd0630ae0d944165407e2dec
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68027335"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Esercitazione: Usare l'autenticazione di Azure Active Directory con SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questa esercitazione illustra come configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux per supportare l'autenticazione di Active Directory (AD), detta anche autenticazione integrata. Per una panoramica, vedere [Autenticazione di Active Directory per SQL Server in Linux](sql-server-linux-active-directory-auth-overview.md).

Questa esercitazione è costituita dalle attività seguenti:

> [!div class="checklist"]
> * Aggiungere l'host di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] al dominio di Active Directory
> * Creare un utente di Active Directory per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e impostare il nome dell'entità servizio (SPN)
> * Configurare il keytab del servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
> * Proteggere il file keytab
> * Configurare SQL Server per l'uso del file keytab per l'autenticazione Kerberos
> * Creare account di accesso basati su AD in Transact-SQL
> * Connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando l'autenticazione di Active Directory

## <a name="prerequisites"></a>Prerequisites

Prima di configurare l'autenticazione di Active Directory, è necessario:

* Configurare un controller di dominio di Active Directory (Windows) nella rete  
* Installare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server (SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> Aggiungere l'host di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] al dominio di Active Directory

È necessario aggiungere l'host di SQL Server in Linux a un controller di dominio Active Directory. Aggiungere un host di SQL Server in Linux a un dominio di Active DirectoryPer informazioni sull'aggiunta a un dominio Active Directory, vedere [Aggiungere un host di SQL Server in Linux a un dominio di Active Directory](sql-server-linux-active-directory-join-domain.md).

## <a id="createuser"></a> Creare un utente di Active Directory (o un account del servizio gestito) per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e impostare il nome dell'entità servizio (SPN)

> [!NOTE]
> Nella procedura seguente viene usato il [nome di dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Se si è in **Azure**, è necessario **[crearne uno](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** prima di procedere.

1. Nel controller di dominio eseguire il comando di PowerShell [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) per creare un nuovo utente di Active Directory con una password che non scade mai. L'esempio seguente assegna all'account il nome `mssql`, ma si può scegliere un nome qualsiasi. Verrà chiesto di immettere una nuova password per l'account.

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > Come misura di sicurezza, è consigliabile avere un account AD dedicato per SQL Server, in modo che le credenziali di SQL Server non siano condivise con altri servizi che usano lo stesso account. Tuttavia, se si vuole è possibile riutilizzare un account AD esistente se se ne conosce la password (necessaria per generare un file keytab nel passaggio successivo).

2. Impostare il nome dell'entità servizio (SPN) per l'account usando lo strumento **setspn.exe**. Il nome SPN deve essere formattato esattamente come specificato nell'esempio seguente. È possibile trovare il nome di dominio completo del computer host di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] eseguendo `hostname --all-fqdns` nell'host di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La porta TCP deve essere la 1433, a meno che [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non sia stato configurato per l'uso di un numero di porta diverso.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Se viene visualizzato un messaggio di errore, `Insufficient access rights`, verificare con l'amministratore del dominio di avere autorizzazioni sufficienti per impostare un SPN per l'account.
   >
   > Se si cambia la porta TCP in futuro, è necessario eseguire di nuovo il comando **setspn** con il nuovo numero di porta. È anche necessario aggiungere il nuovo SPN al keytab del servizio SQL Server seguendo la procedura descritta nella sezione successiva.

Per altre informazioni, vedere [Registrare un nome dell'entità servizio per le connessioni Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a id="configurekeytab"></a> Configurare il keytab del servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

È possibile configurare i file keytab del servizio SQL Server in due modi diversi. La prima opzione consiste nell'usare un account computer (UPN), mentre la seconda opzione usa un account del servizio gestito nella configurazione del keytab. Entrambi i metodi sono ugualmente funzionali, quindi basta scegliere quello più adatto per l'ambiente in uso.

In entrambi i casi è necessario il nome dell'entità servizio creato nel passaggio precedente, che deve essere registrato nel keytab.

Per configurare il file keytab del servizio SQL Server:

1. Configurare le [voci del keytab SPN](#spn) nella sezione successiva.

1. Aggiungere quindi le voci del [nome dell'entità utente](#upn) (opzione 1) o dell'[account del servizio gestito](#msa) (opzione 2) nel file keytab seguendo le procedure nelle rispettive sezioni.

> [!IMPORTANT]
> Se si cambia la password del nome dell'entità utente o dell'account del servizio gestito o la password dell'account a cui sono assegnati i nomi dell'entità servizio, è necessario aggiornare il keytab con la nuova password e il numero di versione della chiave. Alcuni servizi potrebbero anche cambiare automaticamente le password a rotazione. Esaminare i criteri di rotazione delle password per gli account in questione e allinearli alle attività di manutenzione pianificata per evitare tempi di inattività imprevisti.

### <a id="spn"></a> Voci del keytab SPN

1. Verificare il numero di versione della chiave per l'account di Active Directory creato nel passaggio precedente. In genere è 2, ma potrebbe essere un altro numero intero se la password dell'account è stata cambiata più volte. Nel computer host SQL Server eseguire i comandi seguenti:

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM
   ```

   > [!NOTE]
   > La propagazione dei nomi SPN nel dominio può richiedere diversi minuti, soprattutto se il dominio è di grandi dimensioni. Se viene visualizzato il messaggio di errore `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM`, attendere qualche minuto e riprovare.  

1. Avviare **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Aggiungere le voci keytab per ogni SPN usando i comandi seguenti:

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. Scrivere il keytab in un file e quindi uscire da Ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > Lo strumento **Ktutil** non convalida la password, quindi assicurarsi di immetterla correttamente quando richiesto.

### <a id="upn"></a> Opzione 1: Usare il nome dell'entità utente (UPN) per configurare il keytab

Aggiungere l'account computer al keytab con **Ktutil**. L'account computer (detto anche UPN) è presente in **/etc/krb5.keytab** nel formato `<hostname>$@<realm.com>` (ad esempio, `sqlhost$@CONTOSO.COM`). Copiare queste voci da **/etc/krb5.keytab** a **mssql.keytab**.

1. Avviare **ktuil** con il comando seguente:

   ```bash
   sudo ktutil
   ```

1. Usare il comando **rkt** per leggere tutte le voci di **/etc/krb5.keytab**.

   ```bash
   rkt /etc/krb5.keytab
   ```

1. Quindi, elencare le voci.

   ```bash
   list
   ```

1. Eliminare tutte le voci che non sono UPN in base al numero di slot. Eseguire questa operazione una voce alla volta ripetendo il comando seguente:

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > Quando viene eliminata una voce, ad esempio lo slot 1, tutti i valori scorrono verso l'alto di una posizione per prendere il suo posto. Questo significa che la voce nello slot 2 si sposta nello slot 1 quando la voce dello slot 1 viene eliminata.

1. Elencare nuovamente le voci finché non rimangono solo le voci UPN.

   ```bash
   list
   ```

1. Quando rimangono solo le voci UPN, accodare questi valori a **mssql.keytab**:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. Uscire da **ktutil**.

   ```bash
   quit
   ```

### <a id="msa"></a> Opzione 2:  Usare l'account del servizio gestito per configurare il keytab

Per questa opzione è necessario creare il keytab Kerberos di SQL Server. Deve contenere tutti gli [SPN registrati nel primo passaggio](#spn) e le credenziali dell'account del servizio gestito in cui sono registrati gli SPN. 

1. Dopo aver creato le voci del keytab SPN, eseguire i comandi seguenti da un computer Linux aggiunto a un dominio:

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   In questo passaggio viene visualizzato il numero di versione della chiave per l'account utente a cui è assegnata la proprietà degli SPN. Per la corretta esecuzione di questo passaggio, è necessario che il nome SPN sia stato assegnato all'account del servizio gestito durante la sua creazione. Se l'SPN non è stato assegnato all'account del servizio gestito, il numero di versione della chiave visualizzato sarà relativo all'attuale account proprietario degli SPN e non sarà il valore corretto da usare per la configurazione.  

1. Avviare **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Aggiungere l'account del servizio gestito con i due comandi seguenti:

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. Scrivere il keytab in un file e quindi uscire da Ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. Quando si usa il metodo dell'account del servizio gestito, è necessario impostare un'opzione di configurazione con lo strumento **mssql-conf** per specificare l'account del servizio gestito da usare durante l'accesso al file keytab. Verificare che i valori seguenti siano presenti in **/var/opt/mssql/mssql.conf**.

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > Includere solo il nome dell'account del servizio gestito e non il nome dominio\account.

## <a id="securekeytab"></a> Proteggere il file keytab

Chiunque abbia accesso a questo file keytab può rappresentare SQL Server nel dominio, quindi assicurarsi di limitare l'accesso al file in modo che solo l'account mssql disponga dell'accesso in lettura:

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> Configurare SQL Server per l'uso del file keytab per l'autenticazione Kerberos

Usare la procedura seguente per configurare SQL Server in modo che inizi a usare il file keytab per l'autenticazione Kerberos.

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

Facoltativamente, disabilitare le connessioni UDP al controller di dominio per migliorare le prestazioni. In molti casi, le connessioni UDP hanno sempre esito negativo quando ci si connette a un controller di dominio, quindi è possibile impostare le opzioni di configurazione in **/etc/krb5.conf** in modo da ignorare le chiamate UDP. Modificare **/etc/krb5.conf** e impostare le opzioni seguenti:

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

A questo punto si è pronti per usare gli account di accesso basati su Active Directory in SQL Server come indicato di seguito.

## <a id="createsqllogins"></a> Creare account di accesso basati su AD in Transact-SQL

1. Connettersi a SQL Server e creare un nuovo account di accesso basato su Active Directory:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. Verificare che l'account di accesso sia ora elencato nella vista del catalogo di sistema [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md):

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> Connettersi a SQL Server usando l'autenticazione di Active Directory

Accedere a un computer client usando le credenziali del proprio dominio. A questo punto è possibile connettersi a SQL Server senza immettere nuovamente la password usando l'autenticazione di Active Directory. Se si crea un account di accesso per un gruppo di Active Directory, qualsiasi utente di Active Directory che sia membro di tale gruppo potrà connettersi nello stesso modo.

Lo specifico parametro della stringa di connessione che indica ai client di usare l'autenticazione di Active Directory dipende dal driver in uso. Considerare gli esempi nelle sezioni riportate di seguito.

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>sqlcmd in un client Linux aggiunto a un dominio

Accedere a un client Linux aggiunto al dominio usando **ssh** e le credenziali del dominio:

```bash
ssh -l user@contoso.com client.contoso.com
```

Assicurarsi di aver installato il pacchetto [mssql-tools](sql-server-linux-setup-tools.md), quindi connettersi usando **sqlcmd** senza specificare le credenziali:

```bash
sqlcmd -S mssql-host.contoso.com
```

### <a name="ssms-on-a-domain-joined-windows-client"></a>SSMS in un client Windows aggiunto a un dominio

Accedere a un client Windows aggiunto al dominio usando le credenziali del dominio. Assicurarsi che SQL Server Management Studio sia installato, quindi connettersi all'istanza di SQL Server, ad esempio `mssql-host.contoso.com`, specificando **Autenticazione di Windows** nella finestra di dialogo **Connetti al server**.

### <a name="ad-authentication-using-other-client-drivers"></a>Autenticazione di Active Directory con altri driver client

La tabella seguente contiene alcuni consigli per altri driver client:

| Driver client | Consiglio |
|---|---|
| **JDBC** | Usare l'autenticazione integrata Kerberos per la connessione a SQL Server. |
| **ODBC** | Usare l'autenticazione integrata SQL. |
| **ADO.NET** | Sintassi della stringa di connessione. |

## <a id="additionalconfig"></a> Opzioni di configurazione aggiuntive

Se si usano utilità di terze parti, come [PBIS](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/) o [Centrify](https://www.centrify.com/), per aggiungere l'host Linux al dominio di Active Directory e si vuole forzare SQL Server a usare direttamente la libreria openldap, è possibile configurare l'opzione **disablesssd** con **mssql-conf** come indicato di seguito:

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> Alcune utilità, come **realmd**, installano SSSD, mentre altri strumenti, come PBIS, VAS e Centrify, non lo fanno. Se l'utilità usata per l'aggiunta al dominio di Active Directory non prevede l'installazione di SSSD, è consigliabile impostare l'opzione **disablesssd** su `true`. Anche se non è necessario, poiché SQL Server tenterà di usare SSSD per Active Directory prima di eseguire il fallback al meccanismo openldap, sarebbe più efficiente configurarlo in modo che SQL Server esegua le chiamate a openldap direttamente ignorando il meccanismo SSSD.

Se il controller di dominio supporta LDAPS, è possibile forzare l'esecuzione di tutte le connessioni da SQL Server ai controller di dominio tramite LDAPS. Per verificare che il client sia in grado di contattare il controller di dominio tramite LDAPS, eseguire il comando bash `ldapsearch -H ldaps://contoso.com:3269`. Per impostare SQL Server in modo da usare solo LDAPS, eseguire il comando seguente:

```bash
sudo mssql-conf set network.forcesecureldap true
systemctl restart mssql-server
```

Verrà usato LDAPS su SSSD se l'aggiunta al dominio AD dell'host è stata eseguita tramite il pacchetto SSSD e **disablesssd** non è impostato su true. Se **disablesssd** è impostato su true e lo è anche **forcesecureldap**, il protocollo LDAPS verrà usato sulle chiamate alla libreria openldap eseguite da SQL Server.

### <a name="post-sql-server-2017-cu14"></a>Dopo SQL Server 2017 CU14

A partire da SQL Server 2017 CU14, se SQL Server è stato aggiunto a un controller di dominio di Active Directory usando provider di terze parti ed è configurato per l'uso di chiamate openldap per la ricerca tramite AD generale impostando **disablesssd** su true, è possibile usare anche l'opzione **enablekdcfromkrb5** per forzare SQL Server a usare la libreria krb5 per la ricerca KDC anziché la ricerca DNS inversa per il server KDC.

Questo può essere utile se si vogliono configurare manualmente i controller di dominio con cui SQL Server tenta di comunicare e si usa il meccanismo della libreria openldap tramite l'elenco KDC in **krb5.conf**.

Prima di tutto impostare **disablessd** e **enablekdcfromkrb5conf** su true, quindi riavviare SQL Server:

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

Configurare poi l'elenco KDC in **/etc/krb5.conf** nel modo seguente:

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> Sebbene non sia consigliato, è possibile usare utilità, come **realmd**, che installano SSSD durante l'aggiunta dell'host Linux al dominio, impostando **disablesssd** su true in modo che SQL Server usi openldap anziché SSSD per le chiamate correlate ad Active Directory.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione sono state illustrate le procedure per configurare l'autenticazione di Active Directory con SQL Server in Linux. Si è appreso come:
> [!div class="checklist"]
> * Aggiungere l'host di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] al dominio di Active Directory
> * Creare un utente di Active Directory per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e impostare il nome dell'entità servizio (SPN)
> * Configurare il keytab del servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
> * Creare account di accesso basati su AD in Transact-SQL
> * Connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando l'autenticazione di Active Directory

Esaminare quindi gli altri scenari di sicurezza per SQL Server in Linux.

> [!div class="nextstepaction"]
> [Crittografia delle connessioni a SQL Server in Linux](sql-server-linux-encrypted-connections.md)
