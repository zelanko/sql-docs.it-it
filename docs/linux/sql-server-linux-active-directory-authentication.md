---
title: 'Esercitazione: Autenticazione di Active Directory per SQL Server in Linux'
titleSuffix: SQL Server
description: Questa esercitazione illustra i passaggi di configurazione di autenticazione di AAD per SQL Server in Linux.
author: meet-bhagdev
ms.date: 02/23/2018
ms.author: meetb
manager: craigg
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: d3b3aaf9688d3517127495fe4b963f5b6de56f0f
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/14/2019
ms.locfileid: "57973590"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Esercitazione: Usare l'autenticazione di Active Directory con SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questa esercitazione illustra come configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux per supportare l'autenticazione di Active Directory (AD), noto anche come l'autenticazione. Per una panoramica, vedere [l'autenticazione di Active Directory per SQL Server in Linux](sql-server-linux-active-directory-auth-overview.md).

Questa esercitazione include le attività seguenti:

> [!div class="checklist"]
> * Join [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host al dominio Active Directory
> * Creare un utente di AD per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e impostare SPN
> * Configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab servizio
> * Creare gli account di accesso basato su Active Directory in Transact-SQL
> * Connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando l'autenticazione di AD

> [!NOTE]
>
> Se si vuole configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux per usare un provider di terze parti AD, vedere [usare i provider di Active Directory di terze parti con SQL Server in Linux](./sql-server-linux-active-directory-third-party-providers.md).

## <a name="prerequisites"></a>Prerequisiti

Prima di configurare l'autenticazione di AD, è necessario:

* Impostare un Controller di dominio Active Directory (Windows) nella rete  
* Installare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> Join [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host al dominio Active Directory

Usare la procedura seguente per aggiungere un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host a un dominio di Active Directory:

1. Uso **[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)** per aggiungere il computer host al dominio AD. Se hai già fatto, installare realmd sia pacchetti client Kerberos nel [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] macchina host usando Gestione pacchetti della distribuzione Linux:

   ```bash
   # RHEL
   sudo yum install realmd krb5-workstation

   # SUSE
   sudo zypper install realmd krb5-client

   # Ubuntu
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Se l'installazione del pacchetto client Kerberos richiede un nome dell'area di autenticazione, immettere il nome di dominio in lettere maiuscole.

   > [!NOTE]
   > Questa procedura dettagliata Usa "contoso.com" e "CONTOSO.COM" rispettivamente come area di autenticazione e di dominio i nomi di esempio. È necessario sostituire questi valori con i propri valori. Questi comandi sono tra maiuscole e minuscole, pertanto assicurarsi di che usare lettere maiuscole ovunque venga usato in questa procedura dettagliata.

1. Configurare il [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computer host per usare l'indirizzo IP del controller di dominio Active Directory come un server dei nomi DNS. 

   - **Ubuntu**:

      Modificare il file `/etc/network/interfaces` in modo che l'indirizzo IP del controller di dominio Active Directory sia elencato come server dns. Esempio: 

      ```/etc/network/interfaces
      <...>
      # The primary network interface
      auto eth0
      iface eth0 inet dhcp
      dns-nameservers **<AD domain controller IP address>**
      dns-search **<AD domain name>**
      ```

      > [!NOTE]
      > L'interfaccia di rete (eth0) potrebbe essere differente per diverse macchine. Per individuare quella in uso, eseguire il comando ifconfig e copiare l'interfaccia che ha un indirizzo IP e che ha trasmesso e ricevuto byte.

      Dopo avere modificato questo file, riavviare il servizio di rete:

      ```bash
      sudo ifdown eth0 && sudo ifup eth0
      ```

      Verificare ora che il `/etc/resolv.conf` file contiene una riga simile al seguente:  

      ```/etc/resolv.conf
      nameserver **<AD domain controller IP address>**
      ```

   - **RHEL**:

     Modificare il file `/etc/sysconfig/network-scripts/ifcfg-eth0` (o altro file di configurazione interfaccia a seconda dei casi) in modo che l'indirizzo IP del controller di dominio Active Directory sia elencato come server dns:

     ```/etc/sysconfig/network-scripts/ifcfg-eth0
     <...>
     PEERDNS=no
     DNS1=**<AD domain controller IP address>**
     ```

     Dopo avere modificato questo file, riavviare il servizio di rete:

     ```bash
     sudo systemctl restart network
     ```

     Verificare ora che il `/etc/resolv.conf` file contiene una riga simile al seguente:  

     ```/etc/resolv.conf
     nameserver **<AD domain controller IP address>**
     ```

   - **SLES**:

     Modificare il `/etc/sysconfig/network/config` file in modo che verrà usato l'indirizzo IP controller di dominio Active Directory per le query DNS e il dominio di AD è incluso nell'elenco di ricerca di dominio:

     ```/etc/sysconfig/network/config
     <...>
     NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
     ```

     Dopo avere modificato questo file, riavviare il servizio di rete:

     ```bash
     sudo systemctl restart network
     ```

     Verificare ora che il `/etc/resolv.conf` file contiene una riga simile al seguente:

     ```/etc/resolv.conf
     nameserver **<AD domain controller IP address>**
     ```

1. Aggiunta al dominio

   Dopo aver verificato che il DNS sia configurato correttamente, aggiungere il dominio eseguendo il comando seguente. È necessario eseguire l'autenticazione con un account di AD che abbia privilegi sufficienti in Active Directory per aggiungere un nuovo computer al dominio.

   In particolare, questo comando crea un nuovo account computer in Active Directory, creare il `/etc/krb5.keytab` ospitare file keytab e configurare il dominio in `/etc/sssd/sssd.conf`:

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   <...>
   * Successfully enrolled machine in realm
   ```

   > [!NOTE]
   > Se viene visualizzato un errore, "non sono installati i pacchetti necessari", quindi è necessario installare tali pacchetti usando Gestione pacchetti della distribuzione Linux prima di eseguire il `realm join` nuovo il comando.
   >
   > Se si riceve un errore, "Autorizzazioni insufficienti per accedere al dominio," è necessario verificare con un amministratore di dominio che si dispone di autorizzazioni sufficienti per aggiungere macchine Linux al dominio.
   >
   > Se si riceve un errore, "Rispondi KDC non corrisponde alle aspettative," quindi era possibile non specificare il nome dell'area di autenticazione corrette per l'utente. I nomi dell'area di autenticazione sono tra maiuscole e minuscole, lettere maiuscole in genere e può essere identificati con il comando `realm discover contoso.com`.
   
   > SQL Server Usa SSSD e NSS per eseguire il mapping di account utente e gruppi per gli identificatori di sicurezza (SID). SSSD deve essere configurato e in esecuzione in ordine per SQL Server creare correttamente gli account di accesso di AD. Realmd in genere viene eseguito automaticamente come parte dell'aggiunta al dominio, ma in alcuni casi è necessario eseguire questa operazione separatamente.
   >
   > Consultare quanto segue per configurare [SSSD manualmente](https://access.redhat.com/articles/3023951), e [configurare NSS per lavorare con SSSD](https://access.redhat.com/documentation/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)

5. Verificare che il dominio è configurato in `/etc/krb5.conf`
    ```/etc/krb5.conf
    [libdefaults]
    default_realm = CONTOSO.COM

    [realms]
    CONTOSO.COM = {
    }

    [domain_realm]
    contoso.com = CONTOSO.COM
    .contoso.com = CONTOSO.COM
    ```

  
6. Verificare che ora è possibile raccogliere informazioni relative a un utente dal dominio e che è possibile acquisire un ticket Kerberos come tale utente.

   L'esempio seguente usa **id**,  **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)**, e **[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** comandi per questo oggetto.

   ```bash
   id user@contoso.com
   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM
   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   <...>
   ```

   > [!NOTE]
   > Se `id user@contoso.com` restituisce un valore "Nessuna tale utente," assicurarsi che il servizio SSSD avviato correttamente eseguendo il comando `sudo systemctl status sssd`. Se il servizio è in esecuzione e viene comunque visualizzato l'errore "Nessun utente", provare ad abilitare la registrazione dettagliata per SSSD. Per altre informazioni, vedere la documentazione di Red Hat per [risoluzione dei problemi SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).
   >
   > Se `kinit user@CONTOSO.COM` "risposta KDC non corrisponde alle aspettative durante il recupero delle credenziali iniziale," restituisce un valore assicurarsi che l'area di autenticazione specificata in lettere maiuscole.

Per altre informazioni, vedere la documentazione di Red Hat per [scoperta e aggiunta di domini di identità](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html). 

## <a id="createuser"></a> Creare un utente di AD per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e impostare SPN

  > [!NOTE]
  > La successiva procedura Usa il [nome di dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Se si usa **Azure**, è necessario **[crearlo](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** prima di procedere.

1. Nel controller di dominio, eseguire la [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) comando di PowerShell per creare un nuovo utente di Active Directory con una password che non scade mai. Questo esempio assegna l'account "mssql", ma il nome dell'account può essere liberamente. Verrà richiesto di immettere una nuova password per l'account:

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > È una protezione ottimale per avere un account dedicato AD per SQL Server, in modo che le credenziali di SQL Server non vengono condivise con altri servizi che utilizzano lo stesso account. Tuttavia, è possibile riutilizzare un account AD esistente se si preferisce, se si conosce la password dell'account (obbligatorio per generare un file keytab nel passaggio successivo).

2. Impostare il ServicePrincipalName (SPN) per questo account utilizzando la `setspn.exe` dello strumento. Il nome SPN deve essere formattato esattamente come specificato nell'esempio seguente. È possibile trovare il nome di dominio completo del [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computer host eseguendo `hostname --all-fqdns` nel [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host e la porta TCP deve essere 1433 a meno che non è stato configurato [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per usare un numero di porta diverso.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Se si riceve un errore, "diritti di accesso insufficienti", quindi è necessario contattare l'amministratore di dominio che si dispone di autorizzazioni sufficienti per impostare un nome SPN per questo account.
   >
   > Se si modifica la porta TCP in futuro, quindi è necessario eseguire nuovamente il comando setspn con il nuovo numero di porta. È anche necessario aggiungere il nuovo nome dell'entità servizio a keytab il servizio SQL Server seguendo i passaggi descritti nella sezione successiva.

3. Per altre informazioni, vedere [Registrare un nome dell'entità servizio per le connessioni Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a id="configurekeytab"></a> Configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab servizio

1. Controllare il numero di versione della chiave (kvno) per l'account di Active Directory creato nel passaggio precedente. In genere è 2, ma potrebbe trattarsi di un altro numero intero, se è stata modificata la password dell'account più volte. Nel [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] macchina host, eseguire il comando seguente:

   ```bash
   kinit user@CONTOSO.COM

   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

   > [!NOTE]
   > I nomi SPN possono richiedere alcuni minuti per propagarsi attraverso il dominio, soprattutto se il dominio è di grandi dimensioni. Se viene visualizzato l'errore, "kvno: Server non è stato trovato nel database Kerberos durante il recupero delle credenziali per MSSQLSvc /\*\*\<il nome di dominio completo del computer host\>\*\*:\* \* \< la porta TCP\>\*\*\@CONTOSO.COM ", attendere qualche minuto e riprovare.

2. Crea un file keytab **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)** per l'utente di Active Directory creato nel passaggio precedente. Quando richiesto, immettere la password per tale account di Active Directory.

   ```bash
   sudo ktutil

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

   > [!NOTE]
   > Lo strumento ktutil non convalidare la password, assicurarsi che immettere correttamente.

3. Aggiungere l'account del computer per il keytab con  **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)**. L'account del computer (detto anche un UPN) è presente in `/etc/krb5.keytab` nel formato "\<hostname\>$\@\<realm.com\>" (ad esempio, $ sqlhost\@CONTOSO.COM). Queste voci da verranno copiati `/etc/krb5.keytab` a `mssql.keytab`.

   ```bash
   sudo ktutil

   # Read all entries from /etc/krb5.keytab
   ktutil: rkt /etc/krb5.keytab

   # List all entries
   ktutil: list

   # Delete all entries by their slot number which are not the UPN one at a
   # time.
   # Warning: when an entry is deleted (e.g. slot 1), all values slide up by
   # one to take its place (e.g. the entry in slot 2 moves to slot 1 when slot
   # 1's entry is deleted)
   ktutil: delent <slot num>
   ktutil: delent <slot num>
   ...

   # List all entries to ensure only UPN entries are left
   ktutil: list

   # When only UPN entries are left, append these values to mssql.keytab
   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

4. Chiunque abbia accesso a questo `keytab` file può rappresentare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sul dominio, quindi verificare che è limitare l'accesso per il file in modo che solo il `mssql` account abbia accesso in lettura:

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
   sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
   ```

5. Configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per usare questo `keytab` file per l'autenticazione Kerberos:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
   sudo systemctl restart mssql-server
   ```

6. Facoltativo: Disabilitare le connessioni dell'UDP al controller di dominio per migliorare le prestazioni. In molti casi, le connessioni di UDP avrà sempre esito negativo quando ci si connette a un controller di dominio, pertanto è possibile impostare le opzioni di configurazione `/etc/krb5.conf` per ignorare le chiamate UDP. Modifica `/etc/krb5.conf` e impostare le opzioni seguenti:

   ```/etc/krb5.conf
   [libdefaults]
   udp_preference_limit=0
   ```

## <a id="createsqllogins"></a> Creare gli account di accesso basato su Active Directory in Transact-SQL

1. Connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e creare un account di accesso di nuovo, basata su Active Directory:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

2. Verificare che l'account di accesso viene ora elencata nel [Sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista del catalogo di sistema:

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> Connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando l'autenticazione di AD

Accedere a un computer client usando le credenziali di dominio. A questo punto è possibile connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] senza immettere di nuovo la password, usando l'autenticazione di AD. Se si crea un account di accesso per un gruppo di Active Directory, qualsiasi utente AD è un membro del gruppo possa connettersi allo stesso modo.

Il parametro della stringa di connessione specifiche per i client di usare l'autenticazione AD dipende dal driver in uso. Si considerino gli esempi seguenti:

* `sqlcmd` in un client Linux appartenenti a un dominio

   Accedere a un client Linux aggiunti al dominio usando `ssh` e le credenziali di dominio:

   ```bash
   ssh -l user@contoso.com client.contoso.com
   ```

   Assicurarsi di aver installato il [mssql-tools](sql-server-linux-setup-tools.md) del pacchetto e quindi connettersi tramite `sqlcmd` senza specificare alcuna credenziale:

   ```bash
   sqlcmd -S mssql-host.contoso.com
   ```

* SQL Server Management Studio in un client di Windows aggiunti a un dominio

   Accedere a un client Windows appartenenti a un dominio usando le credenziali di dominio. Assicurarsi che [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] sia installato e quindi connettersi alle [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] istanza (ad esempio, "mssql-host.contoso.com"), specificando **l'autenticazione di Windows** nel **Connetti al Server** finestra di dialogo.

* Autenticazione di Active Directory con altri driver di client

  * JDBC: [Tramite l'autenticazione integrata Kerberos di connessione SQL Server](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server)
  * ODBC: [Uso dell'autenticazione integrata](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)
  * ADO.NET: [Sintassi della stringa di connessione](https://msdn.microsoft.com/library/system.data.sqlclient.sqlauthenticationmethod(v=vs.110).aspx)

## <a name="performance-improvements"></a>Miglioramenti alle prestazioni
Se si nota che ricerche di account Active Directory richiede un po' di tempo e che sono stati verificati è la configurazione di AD è valida con i passaggi descritti in [Usa autenticazione di Active Directory con SQL Server in Linux tramite i provider di terze parti AD](sql-server-linux-active-directory-third-party-providers.md), è possibile aggiungere il le righe di sotto di `/var/opt/mssql/mssql.conf` per ignorare le chiamate SSSD e usare direttamente le chiamate LDAP.

```/var/opt/mssql/mssql.conf
[network]
disablesssd = true
```

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
