---
title: "Esercitazione: Usare l'autenticazione di AD per SQL Server in Linux"
titleSuffix: SQL Server
description: Questa esercitazione illustra la procedura di configurazione per l'autenticazione di AD per SQL Server in Linux.
author: Dylan-MSFT
ms.author: Dylan.Gray
ms.reviewer: rothja
ms.date: 04/01/2019
manager: craigg
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 5e75a0315c0e632e9637ad1f1467acc90dc586cf
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59240779"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Esercitazione: Usare l'autenticazione di Active Directory con SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questa esercitazione illustra come configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux per supportare l'autenticazione di Active Directory (AD), noto anche come l'autenticazione. Per una panoramica, vedere [l'autenticazione di Active Directory per SQL Server in Linux](sql-server-linux-active-directory-auth-overview.md).

Questa esercitazione include le attività seguenti:

> [!div class="checklist"]
> * Join [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host al dominio Active Directory
> * Creare un utente di AD per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e impostare SPN
> * Configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab servizio
> * Proteggere il file keytab
> * Configurare SQL Server per usare il file keytab per l'autenticazione Kerberos
> * Creare gli account di accesso basato su Active Directory in Transact-SQL
> * Connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando l'autenticazione di AD

## <a name="prerequisites"></a>Prerequisiti

Prima di configurare l'autenticazione di AD, è necessario:

* Impostare un Controller di dominio Active Directory (Windows) nella rete  
* Installazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server (SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> Join [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host al dominio Active Directory

È necessario aggiungere l'host di SQL Server su Linux con un controller di dominio Active Directory. Per informazioni su come aggiungere un dominio active directory, vedere [Join SQL Server in un host Linux a un dominio di Active Directory](sql-server-linux-active-directory-join-domain.md).

## <a id="createuser"></a> Creare l'utente di Active Directory (o account del servizio gestito) per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e impostare SPN

> [!NOTE]
> La procedura seguente usa il [nome di dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Se si usa **Azure**, è necessario **[crearlo](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** prima di procedere.

1. Nel controller di dominio, eseguire la [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) comando di PowerShell per creare un nuovo utente di Active Directory con una password che non scade mai. Nell'esempio seguente i nomi di account `mssql`, ma il nome dell'account può essere liberamente. Verrà chiesto di immettere una nuova password per l'account.

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > È una protezione ottimale per avere un account dedicato AD per SQL Server, in modo che le credenziali di SQL Server non vengono condivise con altri servizi che utilizzano lo stesso account. Tuttavia, è possibile riutilizzare un account AD esistente, facoltativamente, se si conosce la password dell'account (che è obbligatorio per generare un file keytab nel passaggio successivo).

2. Impostare il ServicePrincipalName (SPN) per questo account utilizzando la **setspn.exe** dello strumento. Il nome SPN deve essere formattato esattamente come specificato nell'esempio seguente. È possibile trovare il nome di dominio completo del [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computer host eseguendo `hostname --all-fqdns` nel [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host. La porta TCP deve essere 1433, a meno che non è stato configurato [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per usare un numero di porta diverso.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Se si riceve un errore, `Insufficient access rights`, rivolgersi all'amministratore di dominio che si dispone di autorizzazioni sufficienti per impostare un nome SPN per questo account.
   >
   > Se si modifica la porta TCP in futuro, è necessario eseguire la **setspn** comando nuovamente con il nuovo numero di porta. È anche necessario aggiungere il nuovo nome dell'entità servizio a keytab il servizio SQL Server seguendo i passaggi descritti nella sezione successiva.

Per altre informazioni, vedere [Registrare un nome dell'entità servizio per le connessioni Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a id="configurekeytab"></a> Configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab servizio

Esistono due diversi modi per configurare i file keytab del servizio SQL Server. La prima opzione consiste nell'usare un account del computer (UPN), mentre il secondo metodo prevede un Account di servizio gestiti (MSA) nella configurazione keytab. Entrambi i meccanismi sono ugualmente funzionali ed è possibile scegliere il metodo adatto per l'ambiente.

In entrambi i casi, è necessario il nome SPN creato nel passaggio precedente e il nome SPN deve essere registrato nel keytab.

Per configurare il file keytab del servizio SQL Server:

1. Configurare il [voci keytab SPN](#spn) nella sezione successiva.

1. Quindi entrambi [aggiungere UPN](#upn) (opzione 1) o [MSA](#msa) voci (opzione 2) nel file keytab seguendo i passaggi descritti nelle rispettive sezioni.

> [!IMPORTANT]
> Se si cambia la password per l'UPN/MSA o viene modificata la password per l'account che i nomi SPN vengono assegnati a, è necessario aggiornare il keytab con la nuova password e il numero di versione chiave (KVNO). Alcuni servizi potrebbero anche far ruotare le password automaticamente. Esaminare eventuali criteri di rotazione delle password per gli account in questione e allinearle con attività di manutenzione pianificata per evitare tempo di inattività imprevisto.

### <a id="spn"></a> Voci keytab SPN

1. Controllare il numero di versione chiave (KVNO) per l'account di Active Directory creato nel passaggio precedente. In genere è 2, ma potrebbe trattarsi di un altro numero intero, se è stata modificata la password dell'account più volte. Nel computer host SQL Server, eseguire i comandi seguenti:

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

   > [!NOTE]
   > I nomi SPN possono richiedere alcuni minuti per propagarsi attraverso il dominio, soprattutto se il dominio è di grandi dimensioni. Se viene visualizzato l'errore, `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM`attendere qualche minuto e riprovare.  

1. Avviare **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Aggiungere le voci keytab per ogni nome SPN usando i comandi seguenti:

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac -sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac -sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. Scrivere il keytab in un file e uscire da ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > Il **ktutil** strumento non convalida la password, assicurarsi immetterlo correttamente quando viene richiesto.

### <a id="upn"></a> Opzione 1: Utilizzo di UPN per configurare il keytab

Aggiungere l'account del computer per il keytab con **ktutil**. L'account del computer (detto anche un UPN) è presente in **/etc/krb5.keytab** nel formato `<hostname>$@<realm.com>` (ad esempio, `sqlhost$@CONTOSO.COM`). Copiare queste voci dal **/etc/krb5.keytab** al **mssql.keytab**.

1. Avviare **ktuil** con il comando seguente:

   ```bash
   sudo ktutil
   ```

1. Usare la **rkt** comando per la lettura di tutte le voci dal **/etc/krb5.keytab**.

   ```bash
   rkt /etc/krb5.keytab
   ```

1. Successivamente, elencare le voci.

   ```bash
   list
   ```

1. Eliminare tutte le voci per il numero di slot che non sono l'UPN. Eseguire questo uno alla volta, ripetere il comando seguente:

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > Quando viene eliminata una voce, ad esempio nello slot 1, tutti i valori a tendina da uno a sostituirla. Ciò significa che la voce nello slot 2 Sposta nello slot 1 quando viene eliminata la voce nello slot 1.

1. Elencare le voci di nuovo fino a quando non vengono lasciate solo le voci UPN.

   ```bash
   list
   ```

1. Quando vengono lasciate solo le voci UPN, aggiungere tali valori a **mssql.keytab**:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. Quit **ktutil**.

   ```bash
   quit
   ```

### <a id="msa"></a> Opzione 2:  Utilizzo di account del servizio gestito per configurare il keytab

Per l'opzione account del servizio gestito, è necessario creare keytab Kerberos di SQL Server. Deve contenere tutti i [SPN registrati nel primo passaggio](#spn) e le credenziali per l'account del servizio gestito in cui i nomi SPN vengono registrati. 

1. Dopo il nome SPN keytab vengono creati, eseguire i comandi seguenti da un computer Linux che fa parte del dominio:

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   Questo passaggio consente di visualizzare il KVNO per l'account utente assegnato la proprietà del nome SPN. Per questo passaggio funzionare, il nome SPN deve assegnato all'account del account del servizio gestito durante la sua creazione. Se il nome SPN non è stato assegnato per l'account del servizio gestito, il KVNO visualizzato verrà SPN proprietario dell'account di corrente e non essere corretto da usare per la configurazione.  

1. Avviare **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Aggiungere l'account del servizio gestito con i due comandi seguenti:

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. Scrivere il keytab in un file e uscire da ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. Quando si usa l'approccio account del servizio gestito, un'opzione di configurazione deve essere impostato con il **mssql-conf** dello strumento per specificare l'account del servizio gestito da usare durante l'accesso al file keytab. Verificare i valori seguenti siano **/var/opt/mssql/mssql.conf**.

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > Includere solo il nome di account del servizio gestito e non il nome dominio\account.

## <a id="securekeytab"></a> Proteggere il file keytab

Chiunque abbia accesso a questo file keytab può rappresentare il Server SQL nel dominio, assicurarsi di che limitare l'accesso ai file in modo che solo l'account mssql disponga dell'accesso in lettura:

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> Configurare SQL Server per usare il file keytab per l'autenticazione Kerberos

Utilizzare i seguenti passaggi per configurare il Server SQL per iniziare a usare il file keytab per l'autenticazione Kerberos.

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

Facoltativamente, disabilitare le connessioni dell'UDP al controller di dominio per migliorare le prestazioni. In molti casi, le connessioni di UDP in modo coerente, esito negativo quando ci si connette a un controller di dominio, pertanto è possibile impostare le opzioni di configurazione **/etc/krb5.conf** per ignorare le chiamate UDP. Modificare **/etc/krb5.conf** e impostare le opzioni seguenti:

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

A questo punto, si è pronti a usare gli account di accesso basato su Active Directory in SQL Server come indicato di seguito.

## <a id="createsqllogins"></a> Creare gli account di accesso basato su Active Directory in Transact-SQL

1. Connettersi a SQL Server e creare un account di accesso di nuovo, basata su Active Directory:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. Verificare che l'account di accesso viene ora elencata nel [Sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista del catalogo di sistema:

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> Connettersi a SQL Server usando l'autenticazione di AD

Accedere a un computer client usando le credenziali di dominio. A questo punto è possibile connettersi a SQL Server senza immettere di nuovo la password usando l'autenticazione di AD. Se si crea un account di accesso per un gruppo di Active Directory, qualsiasi utente AD è un membro del gruppo possa connettersi allo stesso modo.

Il parametro della stringa di connessione specifiche per i client di usare l'autenticazione AD dipende dal driver in uso. Si considerino gli esempi nelle sezioni seguenti.

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>SQLCMD in un client Linux appartenenti a un dominio

Accedere a un client Linux aggiunti al dominio usando **ssh** e le credenziali di dominio:

```bash
ssh -l user@contoso.com client.contoso.com
```

Assicurarsi di aver installato il [mssql-tools](sql-server-linux-setup-tools.md) del pacchetto e quindi connettersi tramite **sqlcmd** senza specificare alcuna credenziale:

```bash
sqlcmd -S mssql-host.contoso.com
```

### <a name="ssms-on-a-domain-joined-windows-client"></a>SQL Server Management Studio in un client di Windows aggiunti a un dominio

Accedere a un client Windows appartenenti a un dominio usando le credenziali di dominio. Verificare che sia installato SQL Server Management Studio e quindi connettersi all'istanza di SQL Server (ad esempio, `mssql-host.contoso.com`), specificando **l'autenticazione di Windows** nel **Connetti al Server** finestra di dialogo.

### <a name="ad-authentication-using-other-client-drivers"></a>Autenticazione di Active Directory con altri driver di client

La tabella seguente descrive le raccomandazioni per gli altri driver di client:

| Driver del client | Consiglio |
|---|---|
| **JDBC** | Usare l'autenticazione integrata Kerberos di connessione SQL Server. |
| **ODBC** | Usare l'autenticazione integrata. |
| **ADO.NET** | Sintassi della stringa di connessione. |

## <a id="additionalconfig"></a> Opzioni di configurazione aggiuntive

Se si usa ad esempio le utilità di terze parti [PBI](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/), o [Centrify](https://www.centrify.com/) per aggiungere l'host Linux AD dominio e si vuole forzare il server SQL usando il openldap libreria direttamente, è possibile configurare il **disablesssd** opzione con **mssql-conf** come indicato di seguito:

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> Sono disponibili, ad esempio l'utilità **realmd** quale configurare SSSD, mentre altri strumenti, ad esempio i PBI, VAS e Centrify fare installare SSSD. Se non è stato configurato SSSD con l'utilità utilizzata per unire il dominio di Active Directory, è consigliabile configurare **disablesssd** possibilità `true`. Anche se non è obbligatorio perché SQL Server proverà a usare SSSD per Active Directory prima di eseguire il fallback al meccanismo openldap, sarebbe più efficiente per configurarlo in modo che SQL Server effettua chiamate openldap direttamente esclusione del meccanismo SSSD.

Se il controller di dominio supporta LDAPS, è possibile forzare tutte le connessioni da SQL Server a controller di dominio per essere tramite LDAPS. Per controllare il client può contattare il controller di dominio tramite ldaps, eseguire il seguente comando bash, `ldapsearch -H ldaps://contoso.com:3269`. Per configurare SQL Server da usare solo LDAPS, eseguire il comando seguente:

```bash
sudo mssql-conf set network.forceldaps true
systemctl restart mssql-server
```

Si userà LDAPS su SSSD se Active Directory domain join su host è stato eseguito tramite il pacchetto SSSD e **disablesssd** non è impostata su true. Se **disablesssd** è impostata su true insieme **forceldaps** impostato su true, si userà protocollo LDAPS su chiamate alla libreria openldap eseguite da SQL Server.

### <a name="post-sql-server-2017-cu14"></a>Post SQL Server 2017 CU14

Partire da SQL Server 2017 CU14, se SQL Server è stato aggiunto a un controller di dominio Active Directory usando provider di terze parti ed è configurato per usare openldap chiamate per la ricerca tramite AD generale impostando **disablesssd** per true, è anche possibile usare **enablekdcfromkrb5** opzione per imporre a SQL Server da usare libreria krb5 per ricerca KDC invece di ricerca DNS inversa per il server KDC.

Ciò può essere utile per lo scenario in cui si desidera configurare manualmente i controller di dominio che tenta di comunicare con SQL Server. E si utilizza il meccanismo di libreria openldap usando l'elenco KDC nel **krb5.conf**.

Innanzitutto, impostare **disablessd** e **enablekdcfromkrb5conf** su true e quindi riavviare SQL Server:

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

Configurare quindi nell'elenco KDC **/etc/krb5.conf** come indicato di seguito:

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> Sebbene non sia consigliabile, è possibile usare le utilità, ad esempio **realmd**, impostato durante l'aggiunta di host di Linux per il dominio, durante la configurazione SSSD **disablesssd** su true in modo che usi di SQL Server chiamate OpenLDAP invece di SSSD per Active Directory di chiamate correlate.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato illustrato come configurare l'autenticazione di Active Directory con SQL Server in Linux. Si è appreso come a:
> [!div class="checklist"]
> * Join [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host al dominio Active Directory
> * Creare un utente di AD per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e impostare SPN
> * Configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab servizio
> * Creare gli account di accesso basato su Active Directory in Transact-SQL
> * Connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando l'autenticazione di AD

Successivamente, è possibile esplorare altri scenari di sicurezza per SQL Server in Linux.

> [!div class="nextstepaction"]
>[Crittografia delle connessioni a SQL Server in Linux](sql-server-linux-encrypted-connections.md)
