---
title: Come configurare MSDTC in Linux
description: Questo articolo fornisce una procedura dettagliata per la configurazione di MSDTC in Linux.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 03/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: f4fe81c5e306b059414fe0f2245aca9c9787ee1b
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834017"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>Come configurare Microsoft Distributed Transaction Coordinator (MSDTC) in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo descrive come configurare Microsoft Distributed Transaction Coordinator (MSTDC) in Linux. Supporto MSDTC in Linux è stato introdotto in fase di anteprima di SQL Server 2019.

## <a name="overview"></a>Panoramica

Le transazioni distribuite sono abilitate in SQL Server in Linux con l'introduzione di MSDTC e RPC funzionalità di BizTalk mapper di endpoint all'interno di SQL Server. Per impostazione predefinita, un processo di mapping degli endpoint RPC è in ascolto sulla porta 135 per le richieste RPC in ingresso e fornisce informazioni sui componenti registrati per le richieste remote. Richieste remote possono usare le informazioni restituite dal mapper di endpoint per comunicare con i componenti RPC registrati, ad esempio servizi MSDTC. Un processo richiede privilegi di utente con privilegi avanzati per eseguire l'associazione di porte note (numeri di porta inferiori a 1024) in Linux. Per evitare l'avvio di SQL Server con privilegi a livello radice per il processo RPC endpoint mapper, gli amministratori di sistema devono usare iptables per creare il protocollo NAT per instradare il traffico sulla porta 135 al processo di mapping degli endpoint della SQL Server RPC.

SQL Server 2019 presenta due parametri di configurazione per l'utilità mssql-conf.

| impostazione MSSQL-conf | Descrizione |
|---|---|
| **network.rpcport** | La porta TCP che associa il processo di agente mapping endpoint RPC. |
| **distributedtransaction.servertcpport** | La porta che il server MSDTC è in ascolto. Se non impostato, il servizio MSDTC utilizza una porta temporanea casuale sul riavvio del servizio e le eccezioni del firewall dovrà essere riconfigurato in modo da garantire che il servizio MSDTC possibile la comunicazione. |

Per altre informazioni su queste impostazioni e altre impostazioni MSDTC correlate, vedere [configurare SQL Server in Linux con lo strumento mssql-conf](sql-server-linux-configure-mssql-conf.md#msdtc).

## <a name="supported-msdtc-configurations"></a>Configurazioni supportate di MSDTC

Sono supportate le seguenti configurazioni di MSDTC:

- OLE-TX transazioni distribuite in SQL Server in Linux per provider ODBC.
- Transazioni distribuite XA sono Impostate su SQL Server in Linux usando i provider ODBC e JDBC. Per le transazioni XA deve essere eseguita tramite il provider ODBC, è necessario usare Microsoft ODBC Driver per SQL Server versione 17.3 o successiva.
- Transazioni distribuite nel server collegato.

Per le limitazioni e problemi noti per MSDTC in fase di anteprima, vedere [note sulla versione di anteprima di SQL Server 2019 in Linux](sql-server-linux-release-notes-2019.md#msdtc).

## <a name="msdtc-configuration-steps"></a>Passaggi di configurazione di MSDTC

Esistono tre passaggi per configurare la funzionalità e le comunicazioni MSDTC. Se non vengono eseguiti i passaggi di configurazione necessarie, SQL Server non abiliterà la funzionalità MSDTC.

- Configurare **network.rpcport** e **distributedtransaction.servertcpport** usando mssql-conf.
- Configurare il firewall per consentire la comunicazione sul **distributedtransaction.servertcpport** e la porta 135.
- Configurare il server Linux routing in modo che la comunicazione RPC sulla porta 135 viene reindirizzata a SQL Server **network.rpcport**.

Le sezioni seguenti forniscono istruzioni dettagliate per ogni passaggio.

## <a name="configure-rpc-and-msdtc-ports"></a>Configurare le porte RPC e MSDTC

Configurare innanzitutto **network.rpcport** e **distributedtransaction.servertcpport** usando mssql-conf. Questo passaggio se comuni tra tutte le distribuzioni supportate e specifiche di SQL Server.

1. Usare mssql-conf per impostare il **network.rpcport** valore. Nell'esempio seguente imposta lo 13500.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport 13500
   ```

2. Impostare il **distributedtransaction.servertcpport** valore. Nell'esempio seguente imposta lo 51999.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport 51999
   ```

3. Riavviare SQL Server.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="configure-the-firewall"></a>Configurare il firewall

Il secondo passaggio consiste nel configurare il firewall per consentire la comunicazione sul **servertcpport** e la porta 135.  In questo modo il processo MSDTC per comunicare esternamente ad altri gestori delle transazioni e i coordinatori e il processo di mapping endpoint RPC. I passaggi effettivi per questo variano a seconda della distribuzione di Linux e firewall. 

Nell'esempio seguente viene illustrato come creare queste regole sul **Ubuntu**.

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

L'esempio seguente mostra come è stato possibile eseguire questa operazione per **Red Hat Enterprise Linux (RHEL)** :

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

È importante configurare il firewall prima di configurare routing delle porte nella sezione successiva. Aggiornamento dei firewall, è possibile cancellare le regole di routing di porta in alcuni casi.

## <a name="configure-port-routing"></a>Configurare il routing di porta

Configurare la tabella di routing server Linux in modo che la comunicazione RPC sulla porta 135 viene reindirizzata a SQL Server **network.rpcport**. Meccanismo di configurazione di port forwarding in distribuzione diverso può variare. Le sezioni seguenti forniscono indicazioni per Ubuntu, unità di streaming Enterprise Linux (SLES) e Red Hat Enterprise Linux (RHEL).

### <a name="port-routing-in-ubuntu-and-sles"></a>Porta il routing in Ubuntu e SLES

Ubuntu e SLES non usano i **firewalld** del servizio, pertanto **iptables** regole sono un meccanismo efficiente per raggiungere routing delle porte. Il **iptables** regole potrebbero non persistere durante i riavvii, in modo che i comandi seguenti offrono anche istruzioni per il ripristino delle regole dopo un riavvio.

1. Creare regole di routing per la porta 135. Nell'esempio seguente, la porta 135 viene indirizzata alla porta RPC, 13500, definita nella sezione precedente. Sostituire `<ipaddress>` con l'indirizzo IP del server.

   ```bash
   sudo iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   sudo iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   Il `--comment RpcEndPointMapper` parametro nei comandi precedenti assiste nella gestione di queste regole nei comandi successivi.

2. Visualizzare le regole di routing che è stato creato con il comando seguente:

   ```bash
   sudo iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. Salvare le regole di routing in un file nel computer.

   ```bash
   sudo iptables-save > /etc/iptables.conf
   ```

4. Per ricaricare le regole dopo un riavvio, aggiungere il comando seguente per `/etc/rc.local` (per Ubuntu) o a `/etc/init.d/after.local` (per SLES):

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

   > [!NOTE]
   > È necessario disporre dei privilegi di utente con privilegi avanzati (sudo) per modificare la **Local** oppure **after.local** file.

Il **iptables salvataggio** e **iptables-restore** comandi, insieme con `rc.local` / `after.local` configurazione di avvio, forniscono un meccanismo di base per salvare e ripristinare iptables voci. A seconda della distribuzione di Linux, si potrebbe essere più avanzati o automatizzate le opzioni disponibili. Ad esempio, un'alternativa di Ubuntu è il **permanenti iptables** pacchetto per rendere persistente le voci.

> [!IMPORTANT]
> I passaggi precedenti presuppongono un indirizzo IP fisso. Se viene modificato l'indirizzo IP per l'istanza di SQL Server (a causa di interventi manuali o DHCP), è necessario rimuovere e ricreare le regole di routing se sono state create con iptables. Se è necessario ricreare o eliminare le regole di routing esistente, è possibile usare il comando seguente per rimuovere vecchia `RpcEndPointMapper` regole:
> 
> ```bash
> sudo iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

### <a name="port-routing-in-rhel"></a>Routing in RHEL porta

Nelle distribuzioni che usano **firewalld** servizio, ad esempio Red Hat Enterprise Linux, lo stesso servizio può essere usato per entrambi apertura della porta nel server e l'inoltro alla porta interni. Ad esempio, in Red Hat Enterprise Linux, è consigliabile usare **firewalld** service (tramite **firewall-cmd** utilità di configurazione con `-add-forward-port` o opzioni simili) per creare e gestire porte permanente regole di inoltro anziché iptables.

```bash
sudo firewall-cmd --permanent --add-forward-port=port=135:proto=tcp:toport=13500
sudo firewall-cmd --reload
```

## <a name="verify"></a>Verificare

A questo punto, SQL Server deve essere in grado di partecipare alle transazioni distribuite. Per verificare che SQL Server sia in ascolto, eseguire la **netstat** comando (se si usa RHEL, potrebbe essere necessario installare prima il **net-tools** pacchetto):

```bash
sudo netstat -tulpn | grep sqlservr
```

Si dovrebbe visualizzato un output simile al seguente:

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

Tuttavia, dopo un riavvio, SQL Server non viene avviato in ascolto il **servertcpport** fino a quando la prima transazione distribuita. In questo caso, si vedrebbe non SQL Server in ascolto sulla porta 51999 in questo esempio finché la prima transazione distribuita.

## <a name="configure-authentication-on-rpc-communication-for-msdtc"></a>Configurare l'autenticazione in comunicazione RPC per MSDTC

MSDTC per SQL Server in Linux non usa l'autenticazione in comunicazione RPC per impostazione predefinita. Tuttavia, quando il computer host viene aggiunto a un dominio di Active Directory (AD), è possibile configurare MSDTC per usare la comunicazione RPC autenticata usando seguendo **mssql-conf** impostazioni:

| Impostazione | Descrizione |
|---|---|
| **distributedtransaction.allowonlysecurerpccalls**          | Configurare sicuro solo le chiamate RPC per le transazioni distribuite. |
| **distributedtransaction.fallbacktounsecurerpcifnecessary** | Configurare la protezione che delle chiamate RPC solo per le transazioni distribuite. |
| **distributedtransaction.turnoffrpcsecurity**               | Abilita o disabilita la sicurezza RPC per le transazioni distribuite. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su SQL Server in Linux, vedere [SQL Server in Linux](sql-server-linux-overview.md).
