---
title: Come configurare MSDTC in Linux
description: Questo articolo descrive la procedura dettagliata per la configurazione di MSDTC in Linux.
author: VanMSFT
ms.author: vanto
ms.date: 03/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: c44458e1a68c842b6433d7a137865ae8451c136c
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077613"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>Come configurare Microsoft Distributed Transaction Coordinator (MSDTC) in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo descrive come configurare Microsoft Distributed Transaction Coordinator (MSTDC) in Linux. Il supporto di MSDTC in Linux è stato introdotto nell'anteprima di SQL Server 2019.

## <a name="overview"></a>Panoramica

Le transazioni distribuite vengono abilitate in SQL Server in Linux introducendo la funzionalità di mapper di endpoint MSDTC e RPC all'interno di SQL Server. Per impostazione predefinita, un processo di mapping degli endpoint RPC è in ascolto sulla porta 135 per le richieste RPC in ingresso e fornisce informazioni sui componenti registrati alle richieste remote. Le richieste remote possono usare le informazioni restituite dal mapper di endpoint per comunicare con i componenti RPC registrati, ad esempio i servizi MSDTC. Un processo richiede privilegi avanzati per l'associazione a porte note (numeri di porta inferiori a 1024) in Linux. Per evitare di avviare SQL Server con privilegi root per il processo del mapper di endpoint RPC, gli amministratori di sistema devono usare iptables per creare la conversione NAT (Network Address Translation) per instradare il traffico sulla porta 135 al processo di mapping degli endpoint RPC di SQL Server.

SQL Server 2019 introduce due parametri di configurazione per l'utilità mssq-conf.

| Impostazione di mssql-conf | Descrizione |
|---|---|
| **network.rpcport** | Porta TCP a cui viene associato il processo del mapper di endpoint RPC. |
| **distributedtransaction.servertcpport** | Porta su cui è in ascolto il server MSDTC. Se non è impostata, il servizio MSDTC usa una porta temporanea casuale ai riavvii del servizio e sarà necessario riconfigurare le eccezioni del firewall per garantire che il servizio MSDTC possa continuare le comunicazioni. |

Per altre informazioni su queste impostazioni e altre impostazioni MSDTC correlate, vedere [Configurare SQL Server in Linux con lo strumento mssql-conf](sql-server-linux-configure-mssql-conf.md#msdtc).

## <a name="supported-msdtc-configurations"></a>Configurazioni MSDTC supportate

Sono supportate le configurazioni MSDTC seguenti:

- Transazioni distribuite OLE-TX su SQL Server in Linux per provider ODBC.
- Transazioni distribuite XA su SQL Server in Linux tramite provider JDBC e ODBC. Per eseguire transazioni XA con il provider ODBC, è necessario usare Microsoft ODBC Driver for SQL Server versione 17.3 o successiva.
- Transazioni distribuite nel server collegato.

Per le limitazioni e i problemi noti per MSDTC in anteprima, vedere [Note sulla versione dell'anteprima di SQL Server 2019 in Linux](sql-server-linux-release-notes-2019.md#msdtc).

## <a name="msdtc-configuration-steps"></a>Passaggi di configurazione di MSDTC

Sono previsti tre passaggi per configurare le comunicazioni e la funzionalità di MSDTC. Se i passaggi di configurazione necessari non vengono eseguiti, SQL Server non abiliterà la funzionalità MSDTC.

- Configurare **network.rpcport** e **distributedtransaction.servertcpport** con mssql-conf.
- Configurare il firewall per consentire le comunicazioni su **distributedtransaction.servertcpport** e la porta 135.
- Configurare il routing del server Linux in modo che le comunicazioni RPC sulla porta 135 vengano reindirizzate a **network.rpcport** di SQL Server.

Le sezioni seguenti includono istruzioni dettagliate per ogni passaggio.

## <a name="configure-rpc-and-msdtc-ports"></a>Configurare le porte RPC e MSDTC

Configurare prima di tutto **network.rpcport** e **distributedtransaction.servertcpport** con mssql-conf. Questo passaggio è specifico per SQL Server e comune a tutte le distribuzioni supportate.

1. Usare mssql-conf per impostare il valore di **network.rpcport**. Nell'esempio seguente viene impostato il valore 13500.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport 13500
   ```

2. Impostare il valore di **distributedtransaction.servertcpport**. Nell'esempio seguente viene impostato il valore 51999.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport 51999
   ```

3. Riavviare SQL Server.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="configure-the-firewall"></a>Configurare il firewall

Il secondo passaggio consiste nel configurare il firewall per consentire le comunicazioni su **servertcpport** e la porta 135.  Ciò consente al processo di mapping degli endpoint RPC e al processo MSDTC di comunicare esternamente con altri gestori e coordinatori di transazioni. La procedura effettiva può variare a seconda della distribuzione e del firewall di Linux. 

L'esempio seguente mostra come creare queste regole in **Ubuntu**.

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

L'esempio seguente mostra come eseguire questa operazione in **Red Hat Enterprise Linux (RHEL)** :

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

È importante configurare il firewall prima di configurare il routing delle porte nella sezione successiva. In alcuni casi, l'aggiornamento del firewall può cancellare le regole di routing delle porte.

## <a name="configure-port-routing"></a>Configurare il routing delle porte

Configurare la tabella di routing del server Linux in modo che le comunicazioni RPC sulla porta 135 vengano reindirizzate a **network.rpcport** di SQL Server. Il meccanismo di configurazione per l'inoltro delle porte in una distribuzione diversa può variare. Le sezioni seguenti includono indicazioni per Ubuntu, SUS Enterprise Linux (SLES) e Red Hat Enterprise Linux (RHEL).

### <a name="port-routing-in-ubuntu-and-sles"></a>Routing delle porte in Ubuntu e SLES

Ubuntu e SLES non usano il servizio **firewalld**, quindi le regole di **iptable** rappresentano un meccanismo efficiente per ottenere il routing delle porte. Le regole di **iptable** potrebbero non essere mantenute tra un riavvio e l'altro, quindi i comandi seguenti includono anche istruzioni per il ripristino delle regole dopo un riavvio.

1. Creare regole di routing per la porta 135. Nell'esempio seguente la porta 135 viene indirizzata alla porta RPC 13500 definita nella sezione precedente. Sostituire `<ipaddress>` con l'indirizzo IP del server.

   ```bash
   sudo iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   sudo iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   Il parametro `--comment RpcEndPointMapper` nei comandi precedenti facilita la gestione di queste regole nei comandi successivi.

2. Visualizzare le regole di routing create con il comando seguente:

   ```bash
   sudo iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. Salvare le regole di routing in un file nel computer.

   ```bash
   sudo iptables-save > /etc/iptables.conf
   ```

4. Per ricaricare le regole dopo un riavvio, aggiungere il comando seguente a `/etc/rc.local` (per Ubuntu) o a `/etc/init.d/after.local` (per SLES):

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

   > [!NOTE]
   > Per modificare i file **rc.local** or **after.local**, è necessario disporre di privilegi avanzati (sudo).

I comandi **iptables-save** e **iptables-restore**, insieme alla configurazione di avvio `rc.local`/`after.local`, forniscono un meccanismo di base per salvare e ripristinare le voci di iptables. A seconda della distribuzione Linux potrebbero essere disponibili opzioni più avanzate o automatizzate. Ad esempio, un'alternativa Ubuntu è il pacchetto **iptables-persistent** per rendere persistenti le voci.

> [!IMPORTANT]
> I passaggi precedenti presuppongono un indirizzo IP fisso. Se l'indirizzo IP per l'istanza di SQL Server cambia (a causa di interventi manuali o di DHCP), è necessario rimuovere e ricreare le regole di routing se sono state create con iptables. Se è necessario ricreare o eliminare le regole di routing esistenti, è possibile usare il comando seguente per rimuovere le regole `RpcEndPointMapper` precedenti:
> 
> ```bash
> sudo iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

### <a name="port-routing-in-rhel"></a>Routing delle porte in RHEL

Nelle distribuzioni che usano il servizio **firewalld**, ad esempio Red Hat Enterprise Linux, è possibile usare lo stesso servizio sia per l'apertura della porta nel server che per l'inoltro delle porte interne. Ad esempio, in Red Hat Enterprise Linux, è consigliabile usare il servizio **firewalld** (tramite l'utilità di configurazione **firewall-cmd** con `-add-forward-port` o opzioni simili) per creare e gestire le regole di inoltro delle porte persistenti anziché usare iptables.

```bash
sudo firewall-cmd --permanent --add-forward-port=port=135:proto=tcp:toport=13500
sudo firewall-cmd --reload
```

## <a name="verify"></a>Verifica

A questo punto, SQL Server dovrebbe essere in grado di partecipare alle transazioni distribuite. Per verificare che SQL Server sia in ascolto, eseguire il comando **netstat** (se si usa RHEL, potrebbe essere necessario installare prima il pacchetto **net-tools**):

```bash
sudo netstat -tulpn | grep sqlservr
```

L'output dovrebbe essere simile al seguente:

```bash
tcp 0 0 0.0.0.0:1433 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 127.0.0.1:1434 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:13500 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:51999 0.0.0.0:* LISTEN 13911/sqlservr
tcp6 0 0 :::1433 :::* LISTEN 13911/sqlservr
tcp6 0 0 ::1:1434 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::13500 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::51999 :::* LISTEN 13911/sqlservr
```

Tuttavia, dopo un riavvio, SQL Server non inizia l'ascolto su **servertcpport** fino alla prima transazione distribuita. In questo caso, SQL Server non risulterà in ascolto sulla porta 51999 in questo esempio fino alla prima transazione distribuita.

## <a name="configure-authentication-on-rpc-communication-for-msdtc"></a>Configurare l'autenticazione per le comunicazioni RPC per MSDTC

MSDTC per SQL Server in Linux non usa l'autenticazione per le comunicazioni RPC per impostazione predefinita. Tuttavia, quando il computer host viene aggiunto a un dominio di Active Directory (AD), è possibile configurare MSDTC per l'uso delle comunicazioni RPC autenticate con le impostazioni di **mssql-conf** seguenti:

| Impostazione | Descrizione |
|---|---|
| **distributedtransaction.allowonlysecurerpccalls**          | Configurare solo chiamate RPC protette per le transazioni distribuite. |
| **distributedtransaction.fallbacktounsecurerpcifnecessary** | Configurare la sicurezza delle chiamate RPC per le transazioni distribuite. |
| **distributedtransaction.turnoffrpcsecurity**               | Abilitare o disabilitare la sicurezza RPC per le transazioni distribuite. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su SQL Server in Linux, vedere [SQL Server in Linux](sql-server-linux-overview.md).
