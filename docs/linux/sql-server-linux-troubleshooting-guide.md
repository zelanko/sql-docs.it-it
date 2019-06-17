---
title: Risolvere i problemi di SQL Server in Linux | Microsoft Docs
description: Vengono forniti suggerimenti sulla risoluzione dei problemi per l'uso di SQL Server in Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.openlocfilehash: 6ff0e1eb50f7e7af831ed58b4de05b520fd3f06a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712860"
---
# <a name="troubleshoot-sql-server-on-linux"></a>Risolvere i problemi di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo documento descrive come risolvere i problemi di Microsoft SQL Server in esecuzione in Linux o in un contenitore Docker. La risoluzione dei problemi di SQL Server in Linux, ricordare di esaminare le funzionalità supportate e le limitazioni note nel [SQL Server in note sulla versione di Linux](sql-server-linux-release-notes.md).

> [!TIP]
> Per le risposte alle domande più frequenti, vedere la [SQL Server in Linux FAQ](sql-server-linux-faq.md).

## <a id="connection"></a> Risolvere gli errori di connessione
Se si verificano problemi di connessione a SQL Server a Linux, esistono alcuni aspetti da controllare.

- Se non si riesce a connettersi in locale usando **localhost**, provare a usare invece l'indirizzo IP 127.0.0.1. È possibile che **localhost** non viene correttamente associato a questo indirizzo.

- Verificare che il nome del server o l'indirizzo IP sia raggiungibile dal computer client.

   > [!TIP]
   > Per trovare l'indirizzo IP del computer Ubuntu, è possibile eseguire il comando ifconfig come nell'esempio seguente:
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Per Red Hat, è possibile usare l'indirizzo ip come nell'esempio seguente:
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > Un'eccezione a questa tecnica è correlato alle macchine virtuali di Azure. Per macchine virtuali di Azure [trovare l'indirizzo IP pubblico per la macchina virtuale nel portale di Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect).

- Se applicabile, verificare di avere aperto la porta di SQL Server (valore predefinito 1433) nel firewall.

- Per le VM di Azure, verificare di disporre di un [regola gruppo di sicurezza di rete per la porta di SQL Server predefinita](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote).

- Verificare che il nome utente e la password non contengano eventuali errori di digitazione o spazi aggiuntivi o le maiuscole e minuscole non corretta.

- Provare a impostare in modo esplicito il numero di porta e protocollo con il nome del server simile al seguente: **tcp:servername, 1433**.

- Problemi di connettività di rete possono anche causare timeout ed errori di connessione. Dopo aver verificato le informazioni di connessione e la connettività di rete, provare nuovamente la connessione.

## <a name="manage-the-sql-server-service"></a>Gestire il servizio SQL Server

Le sezioni seguenti illustrano come avviare, arrestare, riavviare e controllare lo stato del servizio SQL Server. 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>Gestire il servizio mssql-server Ubuntu e Red Hat Enterprise Linux (RHEL) 

Controllare lo stato del servizio SQL Server con il seguente comando:

   ```bash
   sudo systemctl status mssql-server
   ```

È possibile arrestare, avviare o riavviare il servizio SQL Server in base alle esigenze usando i comandi seguenti:

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>Gestire l'esecuzione del contenitore Docker mssql

È possibile ottenere l'ID di contenitore e lo stato della versione più recente contenitore Docker di SQL Server creato eseguendo il comando seguente (ID è sotto la **ID del contenitore** colonna):

   ```bash
   sudo docker ps -l
   ```
   
È possibile arrestare o riavviare il servizio SQL Server in base alle esigenze usando i comandi seguenti:
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> Per altri suggerimenti sulla risoluzione dei problemi per Docker, vedere [contenitori Docker di risoluzione dei problemi di SQL Server](sql-server-linux-configure-docker.md#troubleshooting).

## <a name="access-the-log-files"></a>Accedere ai file di log
   
I log del motore di SQL Server per il file /var/opt/mssql/log/errorlog nelle installazioni dei componenti di Linux e Docker. È necessario essere in modalità "superuser" per passare questa directory.

Il programma di installazione Registra qui: / var/rifiutare/mssql/installazione-< timestamp che rappresenta l'ora di installazione > è possibile esplorare i file di log degli errori con qualsiasi strumento compatibile UTF-16, ad esempio 'vim' o 'cat' simile al seguente: 

   ```bash
   sudo cat errorlog
   ```

Se si preferisce, è anche possibile convertire i file in UTF-8 di leggerle con 'altro' o 'meno' con il comando seguente:
   
   ```bash
   sudo iconv -f UTF-16LE -t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>Eventi estesi

È possibile eseguire query di eventi estesi tramite un comando SQL.  Sono disponibili altre informazioni sugli eventi estesi [qui](https://technet.microsoft.com/library/bb630282.aspx):

## <a name="crash-dumps"></a>Dump di arresto anomalo del sistema 

Cercare i dump nella directory dei log in Linux. Controllare le impostazioni di directory /var/opt/mssql/log per i dump di Linux base (. estensione tar.gz2) o dei minidump SQL (con estensione con estensione mdmp)

Per i Core dump 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

Per i dump di SQL 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>Avvio di SQL Server in una configurazione minima o in modalità utente singolo

### <a name="start-sql-server-in-minimal-configuration-mode"></a>Avviare SQL Server in modalità configurazione minima
È utile nel caso in cui l'impostazione di un valore di configurazione, ad esempio un'allocazione eccessiva di memoria, abbia impedito l'avvio del server.
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>Avviare SQL Server in modalità utente singolo
In determinate circostanze, è possibile avviare un'istanza di SQL Server in modalità utente singolo usando l'opzione di avvio -m. Ad esempio, può risultare utile modificare le opzioni di configurazione del server oppure recuperare un database master o un altro database di sistema danneggiato. Ad esempio, è possibile modificare le opzioni di configurazione di server o ripristinare un database master danneggiato o un altro database di sistema   

Avviare SQL Server in modalità utente singolo
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

Avviare SQL Server in modalità utente singolo con SQLCMD
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  Avviare SQL Server in Linux con l'utente "mssql" per evitare problemi di avvio futuri. Esempio "sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]" 

Se è stato avviato per errore SQL Server con un altro utente, è necessario modificare la proprietà del file di database di SQL Server all'utente 'mssql' prima dell'avvio di SQL Server con systemd. Ad esempio, eseguire il comando seguente per modificare la proprietà di tutti i file di database in /var/opt/mssql per l'utente 'mssql',

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="rebuild-system-databases"></a>Ricompilare database di sistema
Come ultima risorsa, è possibile scegliere di rigenerare lo schema e i database modello eseguire il backup per le versioni predefinite.

> [!WARNING]
> Questi passaggi verranno **eliminare tutti i dati di sistema di SQL Server** configurato! Sono incluse informazioni sui database utente (ma non i database utente). Verranno eliminate anche altre informazioni archiviate nel database di sistema, inclusi i seguenti: informazioni di chiave master, tutti i certificati caricati nel master, la password di account di accesso SA, le informazioni relative ai processi da msdb, informazioni di posta elettronica database da msdb e opzioni di sp_configure. Usare solo se si conoscono le implicazioni.

1. Arrestare SQL Server.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Eseguire **sqlservr** con il **force-setup** parametro. 

   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr --force-setup
   ```
   
   > [!WARNING]
   > Vedere l'avviso precedente. Inoltre, è necessario eseguire questo elemento come il **mssql** utente, come illustrato di seguito.

1. Dopo aver visualizzato il messaggio "Ripristino è stato completato", preme CTRL + C. Viene così arrestato SQL Server

1. Riconfigurare le password dell'account SA.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-sa-password
   ```
   
1. Avvio di SQL Server e riconfigurare il server. Sono inclusi il ripristino o ricollegare tutti i database utente.

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="improve-performance"></a>Migliorare le prestazioni

Esistono molti fattori che influiscono sulle prestazioni, tra cui Progettazione database, l'hardware e le richieste di carico di lavoro. Se si intende per migliorare le prestazioni, iniziare esaminando le procedure consigliate, vedere l'articolo [consigliate per le prestazioni e linee guida per la configurazione per SQL Server in Linux](sql-server-linux-performance-best-practices.md). Quindi analizzare alcuni degli strumenti disponibili per la risoluzione dei problemi di prestazioni.

- [Archivio query](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [Viste a gestione dinamica (DMV) del sistema](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [Dashboard delle prestazioni in SQL Server Management Studio](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)

## <a name="common-issues"></a>Problemi comuni

1. Non è possibile connettersi all'istanza di SQL Server remoto.

   Vedere la sezione dell'articolo sulla risoluzione dei problemi [Connetti a SQL Server in Linux](#connection).

2. ERRORE: Nome host deve essere di 15 caratteri o meno.

   Si tratta di un problema noto che si verifica ogni volta che il nome del computer che sta provando a installare il pacchetto Debian di SQL Server è più lungo di 15 caratteri. Non esistono attualmente alcuna soluzione alternativa oltre alla modifica il nome del computer. Un modo per ottenere questo risultato è modificando il file di nome host e il riavvio del computer. Quanto segue [Guida di sito Web](https://www.cyberciti.biz/faq/ubuntu-change-hostname-command/) si illustra in dettaglio.

3. La reimpostazione della password di amministrazione (SA) di sistema.

   Se si dimentica la password di amministratore (SA) di sistema o necessario eseguire questa operazione per altri motivi, seguire questa procedura.

   > [!NOTE]
   > I passaggi seguenti arrestare temporaneamente il servizio SQL Server.

   Accedere al terminale host, eseguire i comandi seguenti e seguire le istruzioni per reimpostare la password dell'amministratore di sistema:

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. Utilizzo di caratteri speciali nella password.

   Se si usano alcuni caratteri della password di account di accesso di SQL Server, è necessario utilizzare caratteri di escape con una barra rovesciata quando vengono usate in un comando nel terminale Linux. Ad esempio, è necessario racchiudere il segno di dollaro ($) ogni volta che si utilizzarlo in uno script shell dei comandi/terminale:

   Non funziona:

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   Funzionamento:

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   Risorse: [Caratteri speciali](https://tldp.org/LDP/abs/html/special-chars.html)
   [Escaping](https://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
