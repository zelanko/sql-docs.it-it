---
title: Usare l'autenticazione di Active Directory (Kerberos)
titleSuffix: Azure Data Studio
description: Informazioni su come abilitare Kerberos per l'uso di autenticazione di Active Directory per Azure Data Studio
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: meet-bhagdev
ms.author: meetb
manager: craigg
ms.openlocfilehash: 02e5e0ba4bd7300d71d95d5e3572ce4e09ac3bd4
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143327"
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>Connettersi a SQL Server utilizzando l'autenticazione di Windows - Kerberos in [!INCLUDE[name-sos](../includes/name-sos-short.md)] 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] supporta la connessione a SQL Server tramite Kerberos.

Per utilizzare l'autenticazione integrata (autenticazione di Windows) in macOS o Linux, è necessario impostare un **ticket Kerberos** collegando l'utente corrente a un account di dominio di Windows 

## <a name="prerequisites"></a>Prerequisiti

- Accedere a un computer nel dominio di Windows per eseguire query verso il controller di dominio Kerberos.
- SQL Server deve essere configurato per consentire l'autenticazione Kerberos. Per il driver client in esecuzione su Unix, l'autenticazione integrata è supportata solo con Kerberos. Sono disponibili ulteriori informazioni sulla configurazione di Sql Server per l'autenticazione tramite Kerberos [qui](https://support.microsoft.com/help/319723/how-to-use-kerberos-authentication-in-sql-server). Devono esistere SPN registrati per ogni istanza di Sql Server a cui si sta tentando di connettersi. I dettagli sul formato dei nomi SPN di SQL Server sono elencati [qui](https://technet.microsoft.com/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)


## <a name="checking-if-sql-server-has-kerberos-setup"></a>Verifica della presenza del setup di Kerberos su Sql Server

Effettuare il login sul computer host di Sql Server. Dal prompt dei comandi Windows, utilizzare il comando `setspn -L %COMPUTERNAME%` per elencare tutti i Nomi Entità Server per l'host. Dovrebbero essere visualizzate voci che iniziano con *MSSQLSvc/HostName.Domain.com* il che indica che Sql Server è registrato con un nome SPN ed è pronto ad accettare l'autenticazione Kerberos.  
- Se non si ha accesso all'host di Sql Server, accedere su qualsiasi altro sistema operativo Windows presente nello stesso dominio Active Directory e utilizzare il comando `setspn -L <SQLSERVER_NETBIOS>` dove <SQLSERVER_NETBIOS> è il nome del computer dell'host di Sql Server.


## <a name="get-the-kerberos-key-distribution-center"></a>Ottenere il centro distribuzione chiavi Kerberos (KDC)

Trovare il valore di configurazione di Kerberos KDC (Key Distribution Center). Eseguire il comando seguente in un computer Windows presente nel dominio di Active Directory: 

Avviare `cmd.exe` ed eseguire `nltest`.

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where "DOMAIN.COMPANY.COM" maps to your domain's name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
Copiare il nome del controller di dominio, che corrisponde al valore di configurazione KDC richiesto; in questo caso dc-33.domain.company.com.

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Collegare il vostro sistema operativo al controller di dominio Active Directory

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

Modificare il file `/etc/network/interfaces` in modo che l'indirizzo IP del controller di dominio Active Directory sia elencato come server dns. Esempio: 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
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

Controllare che il file `/etc/resolv.conf` contenga una riga simile alla seguente:  

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

Controllare che il file `/etc/resolv.conf` contenga una riga simile alla seguente:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- Aggiunta di macOS al Controller di dominio Active Directory seguendo questa procedura:



## <a name="configure-kdc-in-krb5conf"></a>Configurazione KDC in krb5.conf

Modificare il file `/etc/krb5.conf` in un editor di propria scelta. Configurare le chiavi seguenti:


```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

Quindi salvare il file "krb5.conf" e uscire

> [!NOTE]
> Dominio deve essere in lettere maiuscole


## <a name="test-the-ticket-granting-ticket-retrieval"></a>Testare il recupero di Ticket Granting Ticket

Ottenere un Ticket Granting Ticket (TGT) dal KDC.

```bash
kinit username@DOMAIN.COMPANY.COM
```

Consente di visualizzare il ticket disponibile tramite kinit. Se il kinit ha avuto esito positivo, verrà visualizzato un ticket. 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>Connettersi tramite [!INCLUDE[name-sos](../includes/name-sos-short.md)]

* Creare un nuovo profilo di connessione

* Scegliere **Autenticazione di Windows** come tipo di autenticazione

* Completare il profilo di connessione, fare clic su **Connect**

Dopo avere stabilito la connessione, il server viene visualizzato nella barra laterale *server*.
