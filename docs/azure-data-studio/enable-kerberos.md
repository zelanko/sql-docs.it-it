---
title: Usare l'autenticazione di Active Directory (Kerberos)
titleSuffix: Azure Data Studio
description: Informazioni su come abilitare Kerberos per l'uso dell'autenticazione di Active Directory per Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: meet-bhagdev
ms.author: meetb
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 8aa4502fca51ef8dc15fceb119297915a64bc682
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "74957065"
---
# <a name="connect-name-sos-to-your-sql-server-using-windows-authentication---kerberos"></a>Connettere [!INCLUDE[name-sos](../includes/name-sos-short.md)] a SQL Server usando l'autenticazione di Windows - Kerberos 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] supporta la connessione a SQL Server mediante Kerberos.

Per usare l'autenticazione integrata (autenticazione di Windows) in macOS o Linux, è necessario configurare un **ticket Kerberos** che collega l'utente corrente a un account di dominio di Windows. 

## <a name="prerequisites"></a>Prerequisites

- Accesso a un computer aggiunto a un dominio di Windows per eseguire una query sul controller di dominio Kerberos.
- SQL Server deve essere configurato per consentire l'autenticazione Kerberos. Per il driver client in esecuzione su UNIX, l'autenticazione integrata è supportata solo con Kerberos. Per altre informazioni, vedere [Uso dell'autenticazione integrata Kerberos per la connessione a SQL Server](../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md). Devono essere presenti SPN registrati per ogni istanza di SQL Server a cui si intende eseguire la connessione. Per altre informazioni, vedere [Registrazione di un nome SPN](https://technet.microsoft.com/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats).


## <a name="checking-if-sql-server-has-kerberos-setup"></a>Verificare se SQL Server è configurato per Kerberos

Accedere al computer host di SQL Server. Dal prompt dei comandi di Windows usare `setspn -L %COMPUTERNAME%` per elencare tutti i nomi dell'entità servizio per l'host. Dovrebbero essere visualizzate voci che iniziano con MSSQLSvc/HostName.Domain.com, che indicano che SQL Server ha registrato un nome SPN ed è pronto per accettare l'autenticazione Kerberos. 
- Se non si ha accesso all'host di SQL Server, da qualsiasi altro sistema operativo Windows aggiunto allo stesso dominio di Active Directory si può usare il comando `setspn -L <SQLSERVER_NETBIOS>`, dove <SQLSERVER_NETBIOS> è il nome computer dell'host di SQL Server.


## <a name="get-the-kerberos-key-distribution-center"></a>Ottenere il Centro distribuzione chiavi Kerberos

Trovare il valore di configurazione del Centro distribuzione chiavi (KDC) Kerberos. Eseguire il comando seguente in un computer Windows aggiunto al dominio di Active Directory: 

Avviare `cmd.exe` ed eseguire `nltest`.

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where "DOMAIN.COMPANY.COM" maps to your domain's name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
Copiare il nome DC che corrisponde al valore di configurazione di KDC necessario, in questo caso dc-33.domain.company.com

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Aggiungere il sistema operativo al controller dominio Active Directory

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

Modificare il file `/etc/network/interfaces` in modo che l'indirizzo IP del controller di dominio Active Directory sia elencato come dns-nameserver. Ad esempio: 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```

> [!NOTE]
> L'interfaccia di rete (eth0) potrebbe variare per computer diversi. Per individuare quella in uso, eseguire ifconfig e copiare l'interfaccia che ha un indirizzo IP e ha trasmesso e ricevuto byte.

Dopo aver modificato il file, riavviare il servizio di rete:

```bash
sudo ifdown eth0 && sudo ifup eth0
```

Verificare ora che il file `/etc/resolv.conf` contenga una riga simile alla seguente:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
```
   
### <a name="redhat-enterprise-linux"></a>RedHat Enterprise Linux
```bash
sudo yum install realmd krb5-workstation
```

Modificare il file `/etc/sysconfig/network-scripts/ifcfg-eth0` (o un altro file di configurazione dell'interfaccia come appropriato) in modo che l'indirizzo IP del controller di dominio AD sia elencato come server DNS:

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

Dopo aver modificato il file, riavviare il servizio di rete:

```bash
sudo systemctl restart network
```

Verificare ora che il file `/etc/resolv.conf` contenga una riga simile alla seguente:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- Aggiungere macOS al controller di dominio Active Directory eseguendo questa procedura:



## <a name="configure-kdc-in-krb5conf"></a>Configurare KDC in krb5.conf

Modificare il file `/etc/krb5.conf` in un editor di propria scelta. Configurare le chiavi seguenti

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

Salvare quindi il file krb5.conf e uscire

> [!NOTE]
> Il dominio deve in lettere MAIUSCOLE


## <a name="test-the-ticket-granting-ticket-retrieval"></a>Testare il recupero del Ticket Granting Ticket

Ottenere un Ticket Granting Ticket (TGT) da KDC.

```bash
kinit username@DOMAIN.COMPANY.COM
```

Visualizzare i ticket disponibili usando klist. Se il comando kinit ha avuto esito positivo, verrà visualizzato un ticket. 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-name-sos"></a>Eseguire la connessione usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]

* Creare un nuovo profilo di connessione

* Scegliere **Autenticazione di Windows** come tipo di autenticazione

* Completare il profilo di connessione e fare clic su **Connetti**

Dopo il completamento della connessione, il server compare sulla barra laterale *Server*.
