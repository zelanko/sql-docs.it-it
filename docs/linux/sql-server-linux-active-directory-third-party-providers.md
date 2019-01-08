---
title: Usare i provider di Active Directory di terze parti con SQL Server in Linux
titleSuffix: SQL Server
description: Questa esercitazione illustra i passaggi di configurazione per l'autenticazione di Active Directory con i provider di terze parti
author: dylan-MSFT
ms.date: 07/25/2018
ms.author: dygray
manager: mikehab
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AD authentication
ms.openlocfilehash: de28696efd16a2be61864a810b3fd713b1066258
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160569"
---
# <a name="use-third-party-active-directory-providers-with-sql-server-on-linux"></a>Usare i provider di Active Directory di terze parti con SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra come configurare un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un computer host di Linux con l'autenticazione di Active Directory quando si usano provider di Active Directory di terze parti. Sono esempi [PowerBroker Identity Services (PBI)](https://www.beyondtrust.com/), [una sola identità](https://www.oneidentity.com/products/authentication-services/), e [Centrify](https://www.centrify.com/). Questa guida include i passaggi per verificare la configurazione di Active Directory. Non è destinato a illustrare come aggiungere un computer a un dominio. Per istruzioni dettagliate sull'aggiunta di un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host a un dominio usando realmd e SSSD, vedere [autenticazione Usa Active Directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md).

## <a name="prerequisites"></a>Prerequisiti

Prima di configurare l'autenticazione di Active Directory, è necessario configurare un controller di dominio Active Directory, Windows, nella rete. Aggiungere quindi il [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sull'host Linux a un dominio di Active Directory. È possibile usare [PBI](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/), o [Centrify](https://www.centrify.com/).

> [!NOTE]
>
>Questa esercitazione viene usato **`contoso.com`** e **`CONTOSO.COM`** come nomi di dominio e dell'area di autenticazione esempio, rispettivamente. Usa inoltre **`DC1.CONTOSO.COM`** come nell'esempio il nome di dominio del controller di dominio completo. È necessario sostituire questi nomi con i propri valori.

## <a name="check-the-connection-to-a-domain-controller"></a>Controllare la connessione a un controller di dominio

Verificare che sia possibile contattare il controller di dominio con entrambi i nomi brevi e nome completi del dominio:

```bash
ping contoso

ping contoso.com
```

Se uno di questi controlli nome ha esito negativo, aggiornare l'elenco di ricerca di dominio:

- **Ubuntu**

  Modificare il `/etc/network/interfaces` file, in modo che il dominio di Active Directory è nell'elenco di ricerca di dominio: 

  ```/etc/network/interfaces
  <...>
  # The primary network interface
  auto eth0
  iface eth0 inet dhcp
  dns-nameservers **<AD domain controller IP address>**
  dns-search **<AD domain name>**
  ```

  > [!NOTE]  
  > L'interfaccia di rete **eth0**, potrebbero essere diversi per diverse macchine. Per trovare quello in uso, eseguire **ifconfig**. Copiare quindi l'interfaccia con un indirizzo IP e i byte trasmessi e ricevuti.

  Dopo avere modificato questo file, riavviare il servizio di rete:

  ```bash
  sudo ifdown eth0 && sudo ifup eth0
  ```

  Verificare ora che il `/etc/resolv.conf` file contiene una riga simile al seguente:  

  ```/etc/resolv.conf
  search contoso.com com  
  nameserver **<AD domain controller IP address>**
  ```

- **RHEL**

  Modificare il `/etc/sysconfig/network-scripts/ifcfg-eth0` file, in modo che il dominio di Active Directory è nell'elenco di ricerca di dominio. In alternativa, modificare un altro file di configurazione di interfaccia come appropriato:

  ```/etc/sysconfig/network-scripts/ifcfg-eth0
  <...>
  PEERDNS=no
  DNS1=**<AD domain controller IP address>**
  DOMAIN="contoso.com com"
  ```

  Dopo avere modificato questo file, riavviare il servizio di rete:

  ```bash
  sudo systemctl restart network
  ```

  Verificare ora che il `/etc/resolv.conf` file contiene una riga simile al seguente:  

  ```/etc/resolv.conf
  search contoso.com com  
  nameserver **<AD domain controller IP address>**
  ```

  Se è comunque possibile effettuare il ping di controller di dominio, trovare il nome di dominio completo e l'indirizzo IP del controller di dominio. È un nome di dominio di esempio `DC1.CONTOSO.COM`. Aggiungere la seguente voce `/etc/hosts`:

  ```/etc/hosts
  **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
  ```

- **SLES**

  Modificare il `/etc/sysconfig/network/config` file, in modo che l'indirizzo IP controller di dominio Active Directory viene usato per le query DNS e il dominio di Active Directory è nell'elenco di ricerca di dominio:

  ```/etc/sysconfig/network/config
  <...>
  NETCONFIG_DNS_STATIC_SEARCHLIST=""
  NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
  ```

  Dopo avere modificato questo file, riavviare il servizio di rete:

  ```bash
  sudo systemctl restart network
  ```

  Verificare ora che il `/etc/resolv.conf` file contiene una riga simile al seguente:

  ```/etc/resolv.conf
  search contoso.com com
  nameserver **<AD domain controller IP address>**
  ```

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>Verificare che il DNS inverso è configurato correttamente

Questo comando deve restituire il nome di dominio completo dell'host che esegue SQL Server. Ad esempio **`SqlHost.contoso.com`**.

```bash
host **<IP address of SQL Server host>**
# **<reversed IP address>**.in-addr.arpa domain name pointerSqlHost.contoso.com.
```

Se questo comando non restituisce un nome di dominio completo dell'host, o se il nome FQDN non è corretto, aggiungere una voce DNS inversa per sei [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sull'host Linux al server DNS.

## <a name="check-that-your-krb5-configuration-is-correct"></a>Verificare che la configurazione KRB5 sia corretta

Verificare che il `/etc/krb5.conf` sia configurato correttamente. Per la maggior parte dei provider di Active Directory di terze parti, questa configurazione viene eseguita automaticamente. Tuttavia, controllare `/etc/krb5.conf` per i valori seguenti evitare eventuali problemi futuri:

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

## <a name="next-steps"></a>Passaggi successivi

Questo articolo descrive come configurare un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un computer host di Linux con l'autenticazione quando si usano provider di terze parti Active Directory di Active Directory. Per completare la configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux per supportare gli account di Active Directory, seguire le istruzioni in [autenticazione Usa Active Directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md).

> [!div class="nextstepaction"]
> [Usare l'autenticazione di Active Directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md)

> [!NOTE]
>
> È possibile ignorare il **host di partecipare a SQL Server al dominio Active Directory** sezione [autenticazione Usa Active Directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md) come che modifiche appena apportate in questa esercitazione.
