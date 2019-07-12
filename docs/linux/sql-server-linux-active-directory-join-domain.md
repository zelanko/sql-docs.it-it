---
title: Creare un join SQL Server in Linux con Active Directory
titleSuffix: SQL Server
description: ''
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
manager: jroth
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4cee4ca0edcc5a49a34b6c352ae0121bed3b40ca
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834445"
---
# <a name="join-sql-server-on-a-linux-host-to-an-active-directory-domain"></a>Creare un join SQL Server in un host Linux a un dominio di Active Directory

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo offre indicazioni generiche su come aggiungere un computer host SQL Server su Linux a un dominio di Active Directory (AD). Esistono due metodi: usare un pacchetto SSSD predefinito o i provider di Active Directory di terze parti. Sono esempi di prodotti di terze parti domain join [PowerBroker Identity Services (PBI)](https://www.beyondtrust.com/), [una sola identità](https://www.oneidentity.com/products/authentication-services/), e [Centrify](https://www.centrify.com/). Questa guida include i passaggi per verificare la configurazione di Active Directory. Tuttavia, non si tratta di fornire istruzioni su come aggiungere un computer a un dominio quando si usano le utilità di terze parti.

## <a name="prerequisites"></a>Prerequisiti

Prima di configurare l'autenticazione di Active Directory, è necessario configurare un controller di dominio Active Directory, Windows, nella rete. Aggiungere quindi il Server SQL in un host Linux a un dominio di Active Directory.

> [!IMPORTANT]
> La procedura di esempio descritta in questo articolo è per solo come indicazioni. I passaggi effettivi possono variare leggermente nel proprio ambiente in base alla modalità di configurazione dell'ambiente globale. Coinvolgi gli amministratori di sistema e di dominio per l'ambiente per la configurazione specifica, personalizzazione e le operazioni di risoluzione dei problemi.

## <a name="check-the-connection-to-a-domain-controller"></a>Controllare la connessione a un controller di dominio

Verificare che sia possibile contattare il controller di dominio con entrambi i nomi brevi e nome completi del dominio:

```bash
ping contoso
ping contoso.com
```

> [!TIP]
> Questa esercitazione viene usato **contoso.com** e **CONTOSO.COM** come nomi di dominio e dell'area di autenticazione esempio, rispettivamente. Usa inoltre **DC1. CONTOSO.COM** come nell'esempio il nome di dominio del controller di dominio completo. È necessario sostituire questi nomi con i propri valori.

Se uno di questi controlli nome ha esito negativo, aggiornare l'elenco di ricerca di dominio. Le sezioni seguenti forniscono istruzioni per Ubuntu, Red Hat Enterprise Linux (RHEL) e SUSE Linux Enterprise Server (SLES) rispettivamente.

### <a name="ubuntu"></a>Ubuntu

1. Modificare il **/etc/network/interfaces** file, in modo che il dominio di Active Directory è nell'elenco di ricerca di dominio:

   ```/etc/network/interfaces
   # The primary network interface
   auto eth0
   iface eth0 inet dhcp
   dns-nameservers **<AD domain controller IP address>**
   dns-search **<AD domain name>**
   ```

   > [!NOTE]
   > L'interfaccia di rete, `eth0`, potrebbero essere diversi per diverse macchine. Per trovare quello in uso, eseguire **ifconfig**. Copiare quindi l'interfaccia con un indirizzo IP e i byte trasmessi e ricevuti.

1. Dopo avere modificato questo file, riavviare il servizio di rete:

   ```bash
   sudo ifdown eth0 && sudo ifup eth0
   ```

1. Successivamente, verificare che il **/etc/resolv.conf** file contiene una riga simile al seguente:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="rhel"></a>RHEL

1. Modificare il **/etc/sysconfig/network-scripts/ifcfg-eth0** file, in modo che il dominio di Active Directory è nell'elenco di ricerca di dominio. In alternativa, modificare un altro file di configurazione di interfaccia come appropriato:

   ```/etc/sysconfig/network-scripts/ifcfg-eth0
   PEERDNS=no
   DNS1=**<AD domain controller IP address>**
   DOMAIN="contoso.com com"
   ```

1. Dopo avere modificato questo file, riavviare il servizio di rete:

   ```bash
   sudo systemctl restart network
   ```

1. Verificare ora che il **/etc/resolv.conf** file contiene una riga simile al seguente:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

1. Se è comunque possibile effettuare il ping di controller di dominio, trovare il nome di dominio completo e l'indirizzo IP del controller di dominio. È un nome di dominio di esempio **DC1. CONTOSO.COM**. Aggiungere la seguente voce **/e così via/hosts**:

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

### <a name="sles"></a>SLES

1. Modificare il **/etc/sysconfig/network/config** file, in modo che l'indirizzo IP controller di dominio Active Directory viene usato per le query DNS e il dominio di Active Directory è nell'elenco di ricerca di dominio:

   ```/etc/sysconfig/network/config
   NETCONFIG_DNS_STATIC_SEARCHLIST=""
   NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
   ```

1. Dopo avere modificato questo file, riavviare il servizio di rete:

   ```bash
   sudo systemctl restart network
   ```

1. Successivamente, verificare che il **/etc/resolv.conf** file contiene una riga simile al seguente:

   ```/etc/resolv.conf
   search contoso.com com
   nameserver **<AD domain controller IP address>**
   ```

## <a name="join-to-the-ad-domain"></a>Creare un join al dominio di Active Directory

Dopo aver verificato la configurazione di base e la connettività con il controller di dominio, sono disponibili due opzioni per la partecipazione a un computer host SQL Server su Linux con controller di dominio Active Directory:

- [Opzione 1: Usare un pacchetto SSSD](#option1)
- [Opzione 2: Usare le utilità di terze parti openldap provider](#option2)

### <a id="option1"></a> Opzione 1: Usa il pacchetto SSSD aggiunta al dominio di Active Directory

Questo metodo viene aggiunto l'host di SQL Server a un dominio di Active Directory usando **realmd** e **sssd** pacchetti.

> [!NOTE]
> Questo è il metodo preferito di unione di un host Linux a un controller di dominio Active Directory.

Utilizzare la procedura seguente per aggiungere un host di SQL Server a un dominio di Active Directory:

1. Uso [realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join) per aggiungere il computer host al dominio AD. È innanzitutto necessario installare entrambi i **realmd** e pacchetti client Kerberos nel computer host SQL Server usando Gestione pacchetti della distribuzione Linux:

   **RHEL:**

   ```base
   sudo yum install realmd krb5-workstation
   ```

   **SUSE:**

   ```bash
   sudo zypper install realmd krb5-client
   ```

   **Ubuntu:**

   ```bash
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Se l'installazione del pacchetto client Kerberos richiede un nome dell'area di autenticazione, immettere il nome di dominio in lettere maiuscole.

1. Dopo aver confermato che il DNS sia configurato correttamente, aggiungere il dominio eseguendo il comando seguente. È necessario eseguire l'autenticazione con un account di AD che abbia privilegi sufficienti in Active Directory per aggiungere un nuovo computer al dominio. Questo comando crea un nuovo account computer in Active Directory, il **/etc/krb5.keytab** ospitare file keytab, configura il dominio in **/etc/sssd/sssd.conf**e gli aggiornamenti **/etc/krb5.conf**.

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   ```

   Verrà visualizzato il messaggio, `Successfully enrolled machine in realm`.

   Nella tabella seguente sono elencati alcuni messaggi di errore che si potrebbero ricevere e suggerimenti su come risolverli:

   | Messaggio di errore | Recommendation |
   |---|---|
   | `Necessary packages are not installed` | Installare i pacchetti usando Gestione pacchetti della distribuzione Linux prima di eseguire nuovamente il comando di join dell'area di autenticazione. |
   | `Insufficient permissions to join the domain` | Verificare con un amministratore di dominio che si dispone di autorizzazioni sufficienti per aggiungere macchine Linux al dominio. |
   | `KDC reply did not match expectations` | Si potrebbe non avere specificato il nome dell'area di autenticazione corrette per l'utente. Nomi dell'area di autenticazione sono tra maiuscole e minuscole, lettere maiuscole in genere e può essere identificati con l'area di comando Individua contoso.com. |

   SQL Server Usa SSSD e NSS per eseguire il mapping di account utente e gruppi di identificatori di sicurezza (SID). SSSD deve essere configurato e in esecuzione per SQL Server creare correttamente gli account di accesso di AD. **realmd** in genere esegue questa operazione automaticamente come parte dell'aggiunta al dominio, ma in alcuni casi, è necessario eseguire queste operazioni separatamente.

   Per altre informazioni, vedere come [configurare manualmente SSSD](https://access.redhat.com/articles/3023951), e [configurare NSS per lavorare con SSSD](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options).

1. Verificare che ora è possibile raccogliere informazioni relative a un utente dal dominio e che è possibile acquisire un ticket Kerberos come tale utente. L'esempio seguente usa **id**, [kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html), e [klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html) comandi per questo oggetto.

   ```bash
   id user@contoso.com

   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM

   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   ```

   > [!NOTE]
   > - Se **id user@contoso.com**  , restituisce `No such user`, verificare che il servizio SSSD avviato correttamente eseguendo il comando `sudo systemctl status sssd`. Se il servizio è in esecuzione e viene comunque visualizzato l'errore, provare ad abilitare la registrazione dettagliata per SSSD. Per altre informazioni, vedere la documentazione di Red Hat per [risoluzione dei problemi SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).
   >
   > - Se **kinit user@CONTOSO.COM**  restituisce un risultato, `KDC reply did not match expectations while getting initial credentials`, verificare che l'area di autenticazione è specificato in maiuscolo.

Per altre informazioni, vedere la documentazione di Red Hat per [scoperta e aggiunta di domini di identità](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html).

### <a id="option2"></a> Opzione 2: Usare le utilità di terze parti openldap provider

È possibile usare le utilità di terze parti, ad esempio [PBI](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/), o [Centrify](https://www.centrify.com/). Questo articolo illustra i passaggi per ogni singola utilità. È innanzitutto necessario utilizzare una di queste utilità per aggiungere l'host di Linux per SQL Server al dominio prima di continuare in avanti.  

Per tutte le query relative AD SQL Server non Usa codice dell'integratore di sistemi di terze parti o una raccolta. SQL Server esegue sempre una query AD usando chiamate alla libreria openldap direttamente in questa configurazione. Gli integratori di terze parti possono essere usati solo per aggiungere l'host Linux al dominio Active Directory e SQL Server non dispone di qualsiasi comunicazione diretta con queste utilità.

> [!IMPORTANT]
> Vedere le indicazioni per l'uso di **mssql-conf** `network.disablesssd` opzione di configurazione nel **ulteriori opzioni di configurazione** sezione dell'articolo [usare Active L'autenticazione di directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md#additionalconfig).

Verificare che il **/etc/krb5.conf** sia configurato correttamente. Per la maggior parte dei provider di Active Directory di terze parti, questa configurazione viene eseguita automaticamente. Tuttavia, controllare **/etc/krb5.conf** per i valori seguenti evitare eventuali problemi futuri:

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

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>Verificare che il DNS inverso è configurato correttamente

Questo comando deve restituire il nome di dominio completo (FQDN) dell'host che esegue SQL Server. Ad esempio **SqlHost.contoso.com**.

```bash
host **<IP address of SQL Server host>**
```

L'output di questo comando dovrebbe essere simile a `**<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com`. Se questo comando non restituisce il nome di dominio completo dell'host, o se il nome FQDN non è corretto, aggiungere una voce DNS inversa per il Server SQL in un host Linux al server DNS.

## <a name="next-steps"></a>Passaggi successivi

Questo articolo illustra i prerequisiti di configurazione di un Server SQL in un computer host di Linux con l'autenticazione di Active Directory. Per completare la configurazione di SQL Server in Linux per supportare gli account di Active Directory, seguire le istruzioni in [autenticazione Usa Active Directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md).