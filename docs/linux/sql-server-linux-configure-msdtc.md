---
title: Come configurare MSDTC in Linux | Microsoft Docs
description: Questo articolo fornisce una procedura dettagliata per la configurazione di MSDTC in Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 127f39075a1b84b1250a27003efeb28083d1adbd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513192"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>Come configurare Microsoft Distributed Transaction Coordinator (MSDTC) in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo descrive come configurare Microsoft Distributed Transaction Coordinator (MSTDC) in Linux. Supporto MSDTC in Linux è stato introdotto in fase di anteprima di SQL Server 2019.

## <a name="overview"></a>Panoramica

Le transazioni distribuite sono abilitate in SQL Server in Linux con l'introduzione di MSDTC e RPC funzionalità di BizTalk mapper di endpoint all'interno di SQL Server. Per impostazione predefinita, un processo di mapping degli endpoint RPC è in ascolto sulla porta 135 per le richieste RPC in ingresso e le route per i componenti appropriati (ad esempio, il servizio MSDTC). Un processo richiede privilegi di utente con privilegi avanzati per l'associazione di porte note (numeri di porta inferiori a 1024) in Linux. Per evitare l'avvio di SQL Server con privilegi a livello radice per il processo RPC endpoint mapper, gli amministratori di sistema devono usare iptables creare conversione NAT per instradare il traffico sulla porta 135 al processo di mapping degli endpoint della SQL Server RPC.

SQL Server 2019 presenta due parametri di configurazione per l'utilità mssql-conf.

| impostazione MSSQL-conf | Descrizione |
|---|---|
| **Network.rpcport** | La porta TCP che associa il processo di agente mapping endpoint RPC. |
| **Network.servertcpport** | La porta che il server MSDTC è in ascolto. Se non impostato, il servizio MSDTC utilizza una porta temporanea casuale sul riavvio del servizio e le eccezioni del firewall dovrà essere riconfigurato per assicurare che il servizio MSDTC è possibile continuare la comunicazione. |

Per altre informazioni su queste impostazioni e altre impostazioni MSDTC correlate, vedere [configurare SQL Server in Linux con lo strumento mssql-conf](sql-server-linux-configure-mssql-conf.md#msdtc).

## <a name="supported-msdtc-configurations"></a>Configurazioni supportate di MSDTC

Sono supportate le seguenti configurazioni di MSDTC:

- OLE-TX transazioni distribuite in SQL Server in Linux per i provider ODBC e JDBC.
- Transazioni distribuite XA sono Impostate su SQL Server in Linux usando i provider di JDBC.
- Transazioni distribuite nel server collegato.

Per le limitazioni e problemi noti per MSDTC in fase di anteprima, vedere [note sulla versione di anteprima di SQL Server 2019 in Linux](sql-server-linux-release-notes-2019.md#msdtc).

## <a name="msdtc-configuration-steps"></a>Passaggi di configurazione di MSDTC

Esistono tre passaggi per configurare la funzionalità e le comunicazioni MSDTC. Se non vengono eseguiti i passaggi di configurazione necessarie, SQL Server non abiliterà la funzionalità MSDTC.

- Configurare **network.rpcport** e **distributedtransaction.servertcpport** usando mssql-conf.
- Configurare il firewall per consentire la comunicazione sul **rpcport**, **servertcpport**e la porta 135.
- Configurare il server Linux routing in modo che la comunicazione RPC sulla porta 135 viene reindirizzata a SQL Server **network.rpcport**.

Le sezioni seguenti forniscono istruzioni dettagliate per ogni passaggio.

## <a name="configure-rpc-and-msdtc-ports"></a>Configurare le porte RPC e MSDTC

Configurare innanzitutto **network.rpcport** e **distributedtransaction.servertcpport** usando mssql-conf.

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

Il passaggio finale consiste nel configurare il firewall per consentire la comunicazione sul **rpcport**, **servertcpport**e la porta 135.  In questo modo il processo MSDTC per comunicare esternamente ad altri gestori delle transazioni e i coordinatori e il processo di mapping endpoint RPC. I passaggi effettivi per questo variano a seconda della distribuzione di Linux e firewall. 

Nell'esempio seguente viene illustrato come creare queste regole in Ubuntu.

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

L'esempio seguente illustra come eseguire questa operazione in Red Hat Enterprise Linux (RHEL):

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

È importante configurare il firewall prima di configurare routing delle porte nella sezione successiva. Aggiornamento dei firewall, è possibile cancellare le regole di routing di porta in alcuni casi.

## <a name="configure-port-routing"></a>Configurare il routing di porta

Configurare la tabella di routing server Linux in modo che la comunicazione RPC sulla porta 135 viene reindirizzata a SQL Server **network.rpcport**. Meccanismo di configurazione di port forwarding in distribuzione diverso può variare. Nelle distribuzioni che non utilizzano servizio firewalld, regole di iptables sono un meccanismo efficiente per ottenere questo risultato. Esempio di questo tipo distrubution sono v12 SUSE Enterprise Linux e Ubuntu 16.04. Le regole di iptables potrebbero non conservare durante i riavvii, in modo che i comandi seguenti offrono anche istruzioni per il ripristino delle regole dopo un riavvio.

1. Creare regole di routing per la porta 135. Nell'esempio seguente, la porta 135 viene indirizzata alla porta RPC, 13500, definita nella sezione precedente. Sostituire `<ipaddress>` con l'indirizzo IP del server.

   ```bash
   iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   Il `--comment RpcEndPointMapper` parametro nei comandi precedenti assiste nella gestione di queste regole nei comandi successivi.

2. Visualizzare le regole di routing che è stato creato con il comando seguente:

   ```bash
   iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. Salvare le regole di routing in un file nel computer.

   ```bash
   iptables-save > /etc/iptables.conf
   ```

4. Per ricaricare le regole dopo un riavvio, aggiungere il comando seguente per `/etc/rc.local` (per Ubuntu o RHEL) o a `/etc/init.d/after.local` (per SLES):

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

Il **iptables salvataggio** e **iptables ripristino** comandi forniscono un meccanismo di base per salvare e ripristinare le voci di iptables. A seconda della distribuzione di Linux, si potrebbe essere più avanzati o automatizzate le opzioni disponibili. Ad esempio, un'alternativa di Ubuntu è il **permanenti iptables** pacchetto per rendere persistente le voci. 

Nelle distribuzioni che usano service firewalld nello stesso servizio è utilizzabile per entrambi apertura della porta nel server e l'inoltro alla porta interni. In Red Hat Enterprise Linux, ad esempio, si deve usare servizio firewalld (tramite utilità di configurazione di firewall-cmd con - aggiungere-forward-porta o opzioni simili) per creare e gestire permanente regole di port forwarding anziché iptables.

```bash
firewall-cmd --permanent --add-forward-port=port=135:proto=tcp:toport=13500
```

> [!IMPORTANT]
> I passaggi precedenti presuppongono un indirizzo IP fisso. Se viene modificato l'indirizzo IP per l'istanza di SQL Server (a causa di interventi manuali o DHCP), è necessario rimuovere e ricreare le regole di routing se sono state create con iptables. Se è necessario ricreare o eliminare le regole di routing esistente, è possibile usare il comando seguente per rimuovere vecchia `RpcEndPointMapper` regole:
> 
> ```bash
> iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

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

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su SQL Server in Linux, vedere [SQL Server in Linux](sql-server-linux-overview.md).
