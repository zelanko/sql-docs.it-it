---
title: Configurare le impostazioni di SQL Server in Linux | Microsoft Docs
description: Questo articolo descrive come usare lo strumento mssql-conf per configurare le impostazioni di SQL Server in Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.openlocfilehash: 9fd4e35a9fbdd7e0cd3c77fb05ef2f7fdde53c02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719397"
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>Configurare SQL Server in Linux con lo strumento mssql-conf

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

**MSSQL-conf** è uno script di configurazione installato con SQL Server 2017 per Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Ubuntu. È possibile utilizzare questa utilità per impostare i parametri seguenti:

|||
|---|---|
| [Agente](#agent) | Abilitare SQL Server Agent |
| [Regole di confronto](#collation) | Impostare nuove regole di confronto per SQL Server in Linux. |
| [Commenti e suggerimenti dei clienti](#customerfeedback) | Scegliere se SQL Server Invia commenti e suggerimenti a Microsoft. |
| [Profilo di Posta elettronica database](#dbmail) | Impostare il profilo di posta elettronica database predefinito per SQL Server in Linux. |
| [Directory dati predefinita](#datadir) | Modificare la directory predefinita per nuovi file di dati SQL Server database (mdf). |
| [Directory log predefinita](#datadir) | Modifica la directory predefinita per i nuovi file di log (ldf) di database di SQL Server. |
| [Directory predefinita del database master](#masterdatabasedir) | Modifica la directory predefinita per i file di log e database master.|
| [Nome file predefinito del database master](#masterdatabasename) | Modifica il nome del file di database master. |
| [Directory dump predefinita](#dumpdir) | Modificare la directory predefinita per nuove immagini della memoria e altri file sulla risoluzione dei problemi. |
| [Directory log di errore predefinita](#errorlogdir) | Modifica la directory predefinita per i nuovi file di log degli errori di SQL Server, la traccia predefinita Profiler, sistema dello stato della sessione XE e Hekaton sessione XE. |
| [Directory di backup predefinita](#backupdir) | Modificare la directory predefinita per i nuovi file di backup. |
| [Tipo dump](#coredump) | Scegliere il tipo di file dump della memoria dump da raccogliere. |
| [Disponibilità elevata](#hadr) | Abilitare gruppi di disponibilità. |
| [Directory del controllo locale](#localaudit) | Impostare una directory per aggiungere file di controllo locale. |
| [Impostazioni locali](#lcid) | Configurare le impostazioni locali per SQL Server da usare. |
| [Limite di memoria](#memorylimit) | Impostare il limite di memoria per SQL Server. |
| [Porta TCP](#tcpport) | Modificare la porta in cui SQL Server è in ascolto per le connessioni. |
| [TLS](#tls) | Configurare la sicurezza a livello di trasporto. |
| [Flag di traccia](#traceflags) | Impostare i flag di traccia che userà il servizio. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

**MSSQL-conf** è uno script di configurazione che viene installato con [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] per Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Ubuntu. È possibile utilizzare questa utilità per impostare i parametri seguenti:

|||
|---|---|
| [Agente](#agent) | Abilitare SQL Server Agent |
| [Regole di confronto](#collation) | Impostare nuove regole di confronto per SQL Server in Linux. |
| [Commenti e suggerimenti dei clienti](#customerfeedback) | Scegliere se SQL Server Invia commenti e suggerimenti a Microsoft. |
| [Profilo di Posta elettronica database](#dbmail) | Impostare il profilo di posta elettronica database predefinito per SQL Server in Linux. |
| [Directory dati predefinita](#datadir) | Modificare la directory predefinita per nuovi file di dati SQL Server database (mdf). |
| [Directory log predefinita](#datadir) | Modifica la directory predefinita per i nuovi file di log (ldf) di database di SQL Server. |
| [Directory predefinita dei file del database master](#masterdatabasedir) | Modifica la directory predefinita dei file di database master nell'installazione esistente di SQL.|
| [Nome file predefinito del database master](#masterdatabasename) | Modifica il nome del file di database master. |
| [Directory dump predefinita](#dumpdir) | Modificare la directory predefinita per nuove immagini della memoria e altri file sulla risoluzione dei problemi. |
| [Directory log di errore predefinita](#errorlogdir) | Modifica la directory predefinita per i nuovi file di log degli errori di SQL Server, la traccia predefinita Profiler, sistema dello stato della sessione XE e Hekaton sessione XE. |
| [Directory di backup predefinita](#backupdir) | Modificare la directory predefinita per i nuovi file di backup. |
| [Tipo dump](#coredump) | Scegliere il tipo di file dump della memoria dump da raccogliere. |
| [Disponibilità elevata](#hadr) | Abilitare gruppi di disponibilità. |
| [Directory del controllo locale](#localaudit) | Impostare una directory per aggiungere file di controllo locale. |
| [Impostazioni locali](#lcid) | Configurare le impostazioni locali per SQL Server da usare. |
| [Limite di memoria](#memorylimit) | Impostare il limite di memoria per SQL Server. |
| [Microsoft Distributed Transaction Coordinator](#msdtc) | Configurare e risolvere i problemi di MSDTC su Linux. |
| [MLServices EULA](#mlservices-eula) | Accettare per mlservices pacchetti R e Python EULA. Si applica a SQL Server 2019.|
| [outboundnetworkaccess](#mlservices-outbound-access) |Abilitare l'accesso di rete in uscita per [mlservices](sql-server-linux-setup-machine-learning.md) estensioni R, Python e Java.|
| [Porta TCP](#tcpport) | Modificare la porta in cui SQL Server è in ascolto per le connessioni. |
| [TLS](#tls) | Configurare la sicurezza a livello di trasporto. |
| [Flag di traccia](#traceflags) | Impostare i flag di traccia che userà il servizio. |

::: moniker-end

> [!TIP]
> Alcune di queste impostazioni possono inoltre essere configurato con le variabili di ambiente. Per altre informazioni, vedere [le impostazioni di configurazione SQL Server con le variabili di ambiente](sql-server-linux-configure-environment-variables.md).

## <a name="usage-tips"></a>Suggerimenti sull'utilizzo

* Per gruppi di disponibilità AlwaysOn e dischi condivisi cluster, apportare sempre le stesse modifiche di configurazione in ogni nodo.

* Per lo scenario di cluster nel disco condiviso, non tentare di riavviare il **mssql-server** servizio per applicare le modifiche. SQL Server è in esecuzione come un'applicazione. Al contrario, portare la risorsa non in linea e quindi torna online.

* Questi esempi eseguono mssql-conf specificando il percorso completo: **/opt/mssql/bin/mssql-conf**. Se si sceglie di passare a tale percorso, invece, eseguire mssql-conf nel contesto della directory corrente: **. / mssql-conf**.

## <a id="agent"></a> Abilitare SQL Server Agent

Il **sqlagent.enabled** impostazione consente [SQL Server Agent](sql-server-linux-run-sql-server-agent-job.md). Per impostazione predefinita, SQL Server Agent è disabilitato. Se **sqlagent.enabled** non è presente nel file di impostazioni mssql.conf, internamente SQL Server si presuppone che SQL Server Agent è disabilitato.

Per modificare questa impostazione, procedere come segue:

1. Abilitare SQL Server Agent:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

2. Riavviare il servizio SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="collation"></a> Modificare le regole di confronto di SQL Server

Il **set-collation** opzione consente di modificare il valore delle regole di confronto per una delle regole di confronto supportate.

1. Primo [backup di tutti i database utente](sql-server-linux-backup-and-restore-database.md) nel server.

1. Quindi usare il [sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) stored procedure per scollegare i database utente.

1. Eseguire la **set-collation** opzione e seguire le istruzioni:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. L'utilità mssql-conf tenterà di modificare il valore di regole di confronto specificate e riavviare il servizio. Se sono presenti errori, viene eseguito il rollback nuovamente le regole di confronto al valore precedente.

1. Ripristinare i backup dei database utente.

Per un elenco di regole di confronto supportate, eseguire la [Sys. fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) funzione: `SELECT Name from sys.fn_helpcollations()`.

## <a id="customerfeedback"></a> Configurare i suggerimenti dei clienti

Il **telemetry.customerfeedback** viene reimpostata, se SQL Server Invia commenti e suggerimenti a Microsoft o non. Per impostazione predefinita, questo valore è impostato su **true** per tutte le edizioni. Per modificare il valore, eseguire i comandi seguenti:

> [!IMPORTANT]
> È possibile non disattivare commenti degli utenti gratuitamente le edizioni di SQL Server, Express e Developer.

1. Eseguire lo script mssql-conf come radice con il **impostata** comando per **telemetry.customerfeedback**. Nell'esempio seguente consente di disattivare commenti e suggerimenti dei clienti, specificando **false**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Riavviare il servizio SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

Per altre informazioni, vedere [commenti e suggerimenti dei clienti per SQL Server in Linux](sql-server-linux-customer-feedback.md) e il [informativa sulla Privacy di SQL Server](https://go.microsoft.com/fwlink/?LinkID=868444).

## <a id="datadir"></a> Modificare il percorso della directory predefinita dati o di log

Il **filelocation.defaultdatadir** e **filelocation.defaultlogdir** impostazioni modificare la posizione in cui vengono creati i nuovi file di database e log. Per impostazione predefinita, questo percorso è /var/opt/mssql/data. Per modificare queste impostazioni, procedere come segue:

1. Creare la directory di destinazione per il nuovo database i file di dati e di log. L'esempio seguente crea una nuova **/tmp/data** directory:

   ```bash
   sudo mkdir /tmp/data
   ```

1. Modificare il proprietario e il gruppo della directory in cui il **mssql** utente:

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. Usare mssql-conf per modificare la directory dati predefinita con il **impostare** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. Riavviare il servizio SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

1. Tutti i file di database per i nuovi database creati verranno ora essere archiviati nella nuova posizione. Se si desidera modificare il percorso dei file di log (ldf) di nuovi database, è possibile usare il comando "set" di seguito:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. Questo comando presuppone anche che una directory di log/tmp/esista e che è sotto l'utenti e gruppi **mssql**.


## <a id="masterdatabasedir"></a> Modificare il percorso di directory file di database master predefinito

Il **filelocation.masterdatafile** e **filelocation.masterlogfile** impostazione modifiche della posizione in cui il motore di SQL Server cerca i file di database master. Per impostazione predefinita, questo percorso è /var/opt/mssql/data.

Per modificare queste impostazioni, procedere come segue:

1. Creare la directory di destinazione per i nuovi file di log di errore. L'esempio seguente crea una nuova **/tmp/masterdatabasedir** directory:

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. Modificare il proprietario e il gruppo della directory in cui il **mssql** utente:

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. Usare mssql-conf per passare alla directory di database master predefinito per i file di log e dati master con il **impostare** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

   > [!NOTE]
   > Oltre a spostare i dati master e i file di log, si sposta anche il percorso predefinito per tutti gli altri database di sistema.

1. Arrestare il servizio SQL Server:

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Spostare il master. mdf e masterlog.ldf:

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. Avviare il servizio SQL Server:

   ```bash
   sudo systemctl start mssql-server
   ```

   > [!NOTE]
   > Se SQL Server non è possibile trovare i file mdf e Mastlog nella directory specificata, verrà creata automaticamente una copia basata su modelli di database di sistema nella directory specificata e SQL Server verrà avviato correttamente. Tuttavia, metadati, ad esempio i database utente, account di accesso server, i certificati del server, le chiavi di crittografia, processi di SQL agent o vecchia password di account di accesso SA non essere aggiornato nel nuovo database master. È necessario arrestare SQL Server e spostare il vecchio master. mdf e Mastlog. ldf nel nuovo percorso specificato e l'avvio di SQL Server per continuare a usare i metadati esistenti.
 
## <a id="masterdatabasename"></a> Modificare il nome del file di database master

Il **filelocation.masterdatafile** e **filelocation.masterlogfile** impostazione modifiche della posizione in cui il motore di SQL Server cerca i file di database master. È anche possibile utilizzare questo per modificare il nome del file di database e log master. 

Per modificare queste impostazioni, procedere come segue:

1. Arrestare il servizio SQL Server:

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Usare mssql-conf per modificare i nomi di database master previsto per i file di log e dati master con il **impostare** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data/mastlognew.ldf
   ```

   > [!IMPORTANT]
   > È possibile solo modificare il nome del database master e i file di log dopo SQL Server è stato avviato correttamente. Prima dell'esecuzione iniziale, SQL Server si aspetta che i file sia denominato master. mdf e Mastlog. ldf.

1. Modificare il nome del file di dati e log database master 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf
   ```

1. Avviare il servizio SQL Server:

   ```bash
   sudo systemctl start mssql-server
   ```

## <a id="dumpdir"></a> Modificare il percorso predefinito della directory dump

Il **filelocation.defaultdumpdir** impostazione modifica il percorso predefinito in cui la memoria e i dump di SQL vengono generati quando si verifica un arresto anomalo del sistema. Per impostazione predefinita, questi file vengono generati in /var/opt/mssql/log.

Per impostare la nuova posizione, usare i comandi seguenti:

1. Creare la directory di destinazione per i nuovi file di dump. L'esempio seguente crea una nuova **/tmp/dump** directory:

   ```bash
   sudo mkdir /tmp/dump
   ```

1. Modificare il proprietario e il gruppo della directory in cui il **mssql** utente:

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. Usare mssql-conf per modificare la directory dati predefinita con il **impostare** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. Riavviare il servizio SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="errorlogdir"></a> Modificare il percorso di directory predefinito file di log degli errori

Il **filelocation.errorlogfile** la posizione in cui vengono creati il nuovo log degli errori, traccia di profiler predefiniti, sessione di integrità di sistema XE e i file di sessione XE in Hekaton le modifiche alle impostazioni. Per impostazione predefinita, questo percorso è /var/opt/mssql/log. La directory in cui viene impostato il file di log degli errori SQL diventa la directory di log predefinito per gli altri log.

Per modificare queste impostazioni:

1. Creare la directory di destinazione per i nuovi file di log di errore. L'esempio seguente crea una nuova **/tmp/logs** directory:

   ```bash
   sudo mkdir /tmp/logs
   ```

1. Modificare il proprietario e il gruppo della directory in cui il **mssql** utente:

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. Utilizzare mssql-conf per modificare il nome del file di log degli errori predefinito con il **impostare** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. Riavviare il servizio SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```


## <a id="backupdir"></a> Modificare il percorso di directory di backup predefinito

Il **filelocation.defaultbackupdir** impostando il percorso predefinito in cui vengono generati i file di backup delle modifiche. Per impostazione predefinita, questi file vengono generati in /var/opt/mssql/data.

Per impostare la nuova posizione, usare i comandi seguenti:

1. Creare la directory di destinazione per i nuovi file di backup. L'esempio seguente crea una nuova **/tmp/backup** directory:

   ```bash
   sudo mkdir /tmp/backup
   ```

1. Modificare il proprietario e il gruppo della directory in cui il **mssql** utente:

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. Consente di modificare la directory di backup predefinita con il comando "set" mssql-conf:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. Riavviare il servizio SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a> Specificare le impostazioni di dump di base

Se si verifica un'eccezione in uno dei processi di SQL Server, SQL Server viene creato un dump di memoria.

Sono disponibili due opzioni per i dump di controllo del tipo di memoria che SQL Server raccoglie: **coredump.coredumptype** e **coredump.captureminiandfull**. Tali elementi sono correlati a due fasi di acquisizione di core dump. 

La prima acquisizione di fase viene controllata dal **coredump.coredumptype** impostazioni che determinano il tipo di file di dump generati durante un'eccezione. La seconda fase viene attivata quando la **coredump.captureminiandfull** impostazione. Se **coredump.captureminiandfull** è impostata su true, il dump di file specificato da **coredump.coredumptype** viene generato e viene inoltre generato un breve dump secondo. L'impostazione **coredump.captureminiandfull** Disabilita false tentano l'acquisizione di secondo.

1. Decidere se acquisire sia mini che full dump con il **coredump.captureminiandfull** impostazione.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    Valore predefinito: **false**

1. Specificare il tipo di file dump con il **coredump.coredumptype** impostazione.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    Valore predefinito: **miniplus**

    La tabella seguente elenca i possibili **coredump.coredumptype** valori.

    | Type | Descrizione |
    |-----|-----|
    | **mini** | Mini è il tipo di file di dump più piccolo. Usa le informazioni sul sistema di Linux per determinare i thread e i moduli del processo. Il dump contiene solo i moduli e gli stack di thread di ambiente host. Non contiene riferimenti indiretti memoria o alle raccolte globals. |
    | **miniplus** | È simile a mini miniPlus, ma include memoria aggiuntiva. Riconosce le caratteristiche interne di SQLPAL e l'ambiente host, aggiungere le seguenti aree di memoria per il dump:</br></br> -Funzioni globali varie</br> -Tutta la memoria superiori a 64TB</br> -All denominata area trovata **/proc/$ pid e mappe**</br> -Memoria indiretto dal thread e stack</br> -Informazioni thread</br> -Del Teb e associati di Peb</br> -Modulo informazioni</br> -VMM e VAD albero |
    | **filtered** | Progettazione filtrato viene utilizzato un sottrazione basato su tutta la memoria del processo in cui è inclusa solo se esplicitamente esclusi. La progettazione riconosce gli elementi interni di SQLPAL e l'ambiente host, escludendo determinate aree geografiche del dump.
    | **full** | Completa un dump del processo completo che include tutte le aree si trova in **/proc/$ pid e mappe**. Ciò non è controllato dal **coredump.captureminiandfull** impostazione. |

## <a id="dbmail"></a> Impostare il profilo di posta elettronica database predefinito per SQL Server in Linux

Il **sqlpagent.databasemailprofile** consente di impostare il profilo di posta elettronica database predefinito per avvisi di posta elettronica.

```bash
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a> Disponibilità elevata

Il **hadr.hadrenabled** opzione Abilita gruppi di disponibilità nell'istanza di SQL Server. Il seguente comando abilita i gruppi di disponibilità, impostando **hadr.hadrenabled** su 1. È necessario riavviare SQL Server per l'impostazione per rendere effettive.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

Per informazioni su come viene usato con i gruppi di disponibilità, vedere i due argomenti seguenti.

- [Configurare il gruppo di disponibilità AlwaysOn per SQL Server in Linux](sql-server-linux-availability-group-configure-ha.md)
- [Configurare il gruppo di disponibilità con scalabilità in lettura per SQL Server in Linux](sql-server-linux-availability-group-configure-rs.md)


## <a id="localaudit"></a> Directory del set di controllo locale

Il **telemetry.userrequestedlocalauditdirectory** impostazione Abilita controllo locale e consente di impostare la directory log di controllo locale in cui vengono creati.

1. Creare una directory di destinazione per i nuovi log di controllo locale. L'esempio seguente crea una nuova **/tmp/controllo** directory:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. Modificare il proprietario e il gruppo della directory in cui il **mssql** utente:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. Eseguire lo script mssql-conf come radice con il **impostata** comando per **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. Riavviare il servizio SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

Per altre informazioni, vedere [commenti e suggerimenti dei clienti per SQL Server in Linux](sql-server-linux-customer-feedback.md).

## <a id="lcid"></a> Modificare le impostazioni locali di SQL Server

Il **language.lcid** impostando le modifiche delle impostazioni locali di SQL Server a qualsiasi identificatore di lingua supportata (LCID). 

1. Nell'esempio seguente modifica le impostazioni locali sulla lingua francese (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. Riavviare il servizio SQL Server per applicare le modifiche:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a> Impostare il limite di memoria

Il **memory.memorylimitmb** impostazione controlli la quantità memoria fisica (in MB) disponibile in SQL Server. Il valore predefinito è 80% della memoria fisica.

1. Eseguire lo script mssql-conf come radice con il **impostata** comando per **memory.memorylimitmb**. L'esempio seguente modifica la memoria disponibile per SQL Server per 3,25 GB (3328 MB).

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. Riavviare il servizio SQL Server per applicare le modifiche:

   ```bash
   sudo systemctl restart mssql-server
   ```

::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="msdtc"></a> Configurare MSDTC

Il **network.rpcport** e **distributedtransaction.servertcpport** impostazioni vengono usate per configurare Microsoft Distributed Transaction Coordinator (MSDTC). Per modificare queste impostazioni, eseguire i comandi seguenti:

1. Eseguire lo script mssql-conf come radice con il **impostare** comando "network.rpcport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport <rcp_port>
   ```

2. Impostare quindi l'impostazione "distributedtransaction.servertcpport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport <servertcpport_port>
   ```

Oltre a impostare questi valori, è anche necessario configurare il routing e aggiornare il firewall per la porta 135. Per altre informazioni su come eseguire questa operazione, vedere [come configurare MSDTC in Linux](sql-server-linux-configure-msdtc.md).

Esistono diverse altre impostazioni per mssql-conf che è possibile usare per monitorare e risolvere i problemi di MSDTC. Nella tabella seguente vengono descritte brevemente queste impostazioni. Per altre informazioni sul relativo uso, vedere i dettagli nell'articolo del supporto tecnico di Windows [come abilitare la traccia diagnostica per MS DTC](https://support.microsoft.com/help/926099/how-to-enable-diagnostic-tracing-for-ms-dtc-on-a-windows-based-compute).

| impostazione MSSQL-conf | Descrizione |
|---|---|
| distributedtransaction.allowonlysecurerpccalls | Configurare sicuro solo le chiamate RPC per le transazioni distribuite |
| distributedtransaction.fallbacktounsecurerpcifnecessary | Configurare protezione solo per le chiamate RPC per distribuite |transazioni
| distributedtransaction.maxlogsize | DTC transazione dimensioni file di log in MB. Valore predefinito è 64MB |
| distributedtransaction.memorybuffersize | Dimensioni del buffer circolare in cui sono archiviate le tracce. Questa dimensione è espressa in MB e il valore predefinito è 10MB |
| distributedtransaction.servertcpport | Porta del server rpc MSDTC |
| distributedtransaction.trace_cm | Tracce nella gestione connessione |
| distributedtransaction.trace_contact | Analizza il pool di contatto e i contatti |
| distributedtransaction.trace_gateway | Origine di Gateway di tracce |
| distributedtransaction.trace_log | Traccia log |
| distributedtransaction.trace_misc | Tracce che non possono essere suddivise nelle altre categorie |
| distributedtransaction.trace_proxy | Tracce generate nel proxy MSDTC |
| distributedtransaction.trace_svc | Le tracce del servizio e .exe l'avvio del file |
| distributedtransaction.trace_trace | L'infrastruttura di traccia |
| distributedtransaction.trace_util | Analizza le routine di utilità che vengono chiamate da più posizioni |
| distributedtransaction.trace_xa | Origine di traccia di gestione transazioni XA (XATM) |
| distributedtransaction.tracefilepath | Cartella file di traccia devono essere archiviati |
| distributedtransaction.turnoffrpcsecurity | Abilita o disabilita la sicurezza RPC per le transazioni distribuite |

::: moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-eula"></a> Accettare l'EULA MLServices

Aggiunta [dell'apprendimento automatico i pacchetti R o Python](sql-server-linux-setup-machine-learning.md) al database di motore è necessario accettarne le condizioni di licenza per le distribuzioni open source di R e Python. Nella tabella seguente enumera tutti i comandi disponibili o le opzioni relative a mlservices EULA. Lo stesso parametro del contratto di licenza viene usato per R e Python, a seconda dei componenti installati.

```bash
# For all packages: database engine and mlservices
# Setup prompts for mlservices EULAs, which you need to accept
sudo /opt/mssql/bin/mssql-conf setup

# Add R or Python to an existing installation
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml

# Alternative valid syntax
# Adds the EULA section to the INI and sets acceptulam to yes
sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y

# Rescind EULA acceptance and removes the setting
sudo /opt/mssql/bin/mssql-conf unset EULA accepteulaml
```

È anche possibile aggiungere direttamente l'accettazione delle condizioni di licenza di [mssql.conf file](#mssql-conf-format):

```ini
[EULA]
accepteula = Y
accepteulaml = Y
```
:::moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-outbound-access"></a> Abilitare l'accesso alla rete in uscita

L'accesso alla rete in uscita per le estensioni R, Python e Java nel [SQL Server Machine Learning Services](sql-server-linux-setup-machine-learning.md) funzionalità è disabilitata per impostazione predefinita. Per abilitare le richieste in uscita, impostare "outboundnetworkaccess" proprietà Boolean utilizzando mssql-conf.

Dopo aver impostato la proprietà, riavviare il servizio Launchpad di SQL Server per leggere i valori aggiornati dal file INI. Ricorda di un messaggio di riavvio ogni volta che viene modificata un'impostazione di estendibilità.

```bash
# Adds the extensibility section and property.
# Sets "outboundnetworkaccess" to true.
# This setting is required if you want to access data or operations off the server.
sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1

# Turns off network access but preserves the setting
/opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 0

# Removes the setting and rescinds network access
sudo /opt/mssql/bin/mssql-conf unset extensibility.outboundnetworkaccess
```

È anche possibile aggiungere "outboundnetworkaccess" direttamente la [mssql.conf file](#mssql-conf-format):

```ini
[extensibility]
outboundnetworkaccess = 1
```
:::moniker-end

## <a id="tcpport"></a> Modificare la porta TCP

Il **network.tcpport** quando si imposta la porta TCP in cui SQL Server è in ascolto per le connessioni. Per impostazione predefinita, questa porta viene impostata su 1433. Per modificare la porta, eseguire i comandi seguenti:

1. Eseguire lo script mssql-conf come radice con il comando "set" per "network.tcpport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

2. Riavviare il servizio SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

3. Quando ci si connette a SQL Server a questo punto, è necessario specificare la porta personalizzata con una virgola (,) dopo il nome host o indirizzo IP. Per la connessione con SQLCMD, ad esempio, si utilizzerebbe il comando seguente:

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a> Specificare le impostazioni di TLS

Le opzioni seguenti configurare TLS per un'istanza di SQL Server in esecuzione in Linux.

|Opzione |Descrizione |
|--- |--- |
|**network.forceencryption** |Se è 1, quindi [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] forza tutte le connessioni da crittografare. Per impostazione predefinita, questa opzione è 0. |
|**network.tlscert** |Il percorso assoluto per il certificato del file che [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Usa per TLS. Esempio:   `/etc/ssl/certs/mssql.pem`  Il file del certificato deve essere accessibile dall'account mssql. Microsoft consiglia di limitare l'accesso al file usando `chown mssql:mssql <file>; chmod 400 <file>`. |
|**network.tlskey** |Il percorso assoluto della chiave privata del file che [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Usa per TLS. Esempio:  `/etc/ssl/private/mssql.key`  Il file del certificato deve essere accessibile dall'account mssql. Microsoft consiglia di limitare l'accesso al file usando `chown mssql:mssql <file>; chmod 400 <file>`. |
|**network.tlsprotocols** |Elenco delimitato da virgole di cui TLS protocolli consentiti da SQL Server. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tenta sempre di negoziazione del protocollo consentito più attendibili. Se un client non supporta alcun protocollo consentito, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] rifiuta il tentativo di connessione.  Per garantire la compatibilità, sono consentiti tutti i protocolli supportati per impostazione predefinita (1.2, 1.1, 1.0).  Se i client supportano TLS 1.2, si consiglia di consentire solo TLS 1.2. |
|**network.tlsciphers** |Specifica le crittografie consentite dal [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per TLS. Questa stringa debba essere formattata secondo [formato di elenco di pacchetti di crittografia di OpenSSL](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). In generale, non è necessario modificare questa opzione. <br /> Per impostazione predefinita, sono consentite le crittografie seguenti: <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Percorso del file keytab Kerberos |

Per un esempio di utilizzo di impostazioni TLS, vedere [crittografia delle connessioni a SQL Server in Linux](sql-server-linux-encrypted-connections.md).

## <a id="traceflags"></a> Abilitare o disabilitare flag di traccia

Ciò **flag di traccia** opzione Abilita o disabilita i flag di traccia per l'avvio del servizio SQL Server. Per abilitare o disabilitare un flag di traccia usare i comandi seguenti:

1. Abilitare un flag di traccia usando il comando seguente. Ad esempio, per il flag di traccia 1234:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. È possibile abilitare i flag di traccia più specificandoli separatamente:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. In modo analogo, è possibile disabilitare uno o più flag di traccia abilitato, specificarli e aggiungere il **disattivata** parametro:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. Riavviare il servizio SQL Server per applicare le modifiche:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>Rimuovere un'impostazione

Per annullare qualsiasi impostazione effettuata con `mssql-conf set`, chiamare **mssql-conf** con il `unset` opzione e il nome dell'impostazione. In questo modo viene cancellata l'impostazione, in modo efficace restituirlo al relativo valore predefinito.

1. L'esempio seguente cancella i **network.tcpport** opzione.

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. Riavviare il servizio SQL Server.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>Visualizzazione delle impostazioni correnti

Configurato le impostazioni, eseguire il comando seguente per generare il contenuto di visualizzare tutti i **mssql.conf** file:

```bash
sudo cat /var/opt/mssql/mssql.conf
```

Si noti che eventuali impostazioni non illustrate in questo file Usa valori predefiniti. La prossima sezione offre un campione **mssql.conf** file.


## <a id="mssql-conf-format"></a> mssql.conf format

Quanto segue **/var/opt/mssql/mssql.conf** file fornisce un esempio per ogni impostazione. È possibile usare questo formato apportare manualmente modifiche per il **mssql.conf** file in base alle esigenze. Se si modifica manualmente il file, è necessario riavviare SQL Server prima che vengano applicate le modifiche. Usare la **mssql.conf** file con Docker, è necessario disporre di Docker [persistenti i dati](sql-server-linux-configure-docker.md). Prima di tutto aggiungere completa **mssql.conf** file alla directory di host e quindi eseguire il contenitore. È disponibile un esempio di questo tipo in [commenti e suggerimenti dei clienti](sql-server-linux-customer-feedback.md).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```ini
[EULA]
accepteula = Y

[coredump]
captureminiandfull = true
coredumptype = full

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```ini
[EULA]
accepteula = Y
accepteulaml = Y

[coredump]
captureminiandfull = true
coredumptype = full

[distributedtransaction]
servertcpport = 51999

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
rpcport = 13500
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end

## <a name="next-steps"></a>Passaggi successivi

Per usare invece le variabili di ambiente per rendere alcune di queste modifiche di configurazione, vedere [le impostazioni di configurazione SQL Server con le variabili di ambiente](sql-server-linux-configure-environment-variables.md).

Per altri scenari e strumenti di gestione, vedere [gestire SQL Server in Linux](sql-server-linux-management-overview.md).
