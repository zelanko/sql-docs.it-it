---
title: Installare estensioni di linguaggio (Java) di SQL Server in Linux | Microsoft Docs
description: Informazioni su come installare estensioni di linguaggio (Java) di SQL Server su Red Hat, Ubuntu e SUSE.
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8c796d8f445f4cc1b02a0f49d12cde55e0a7ab4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719374"
---
# <a name="install-sql-server-2019-language-extensions-java-on-linux"></a>Installare SQL Server 2019 estensioni del linguaggio (Java) in Linux

Le estensioni del linguaggio sono un componente aggiuntivo per il motore di database. Sebbene sia possibile [installare il motore di database e le estensioni del linguaggio contemporaneamente](#install-all), è consigliabile installare e configurare il motore di database di SQL Server prima di tutto in modo da poter risolvere eventuali problemi prima di aggiungere ulteriori componenti. 

Seguire i passaggi descritti in questo articolo per installare l'estensione del linguaggio Java.

Percorso del pacchetto per le estensioni del linguaggio è nei repository di origine Linux di SQL Server. Se è già configurato repository del codice sorgente per l'installazione del motore di database, è possibile eseguire la **mssql-server-extensibility-java** i comandi di installazione usando la stessa registrazione del repository del pacchetto.

Le estensioni del linguaggio è supportato anche sui contenitori di Linux. Microsoft non fornisce contenitori predefiniti con le estensioni del linguaggio, ma è possibile crearne una dai contenitori di SQL Server usando [un modello di esempio disponibile in GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="uninstall-previous-ctp"></a>Versione CTP precedente di disinstallazione

L'elenco dei pacchetti è stato modificato nelle ultime versioni CTP diversi, generando un minor numero di pacchetti. È consigliabile disinstallare CTP 2.x in modo da rimuovere tutti i pacchetti precedenti prima di installare una versione CTP 3.0. Installazione side-by-side di più versioni non è supportata.

### <a name="1-confirm-package-installation"></a>1. Confermare l'installazione del pacchetto

È possibile verificare l'esistenza di un'installazione precedente come primo passaggio. I file seguenti indicano un'installazione esistente: checkinstallextensibility.sh, exthost, launchpad.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2. Disinstallare i pacchetti di precedente versione CTP 2.x

Disinstallare a livello di pacchetto più basso. Qualsiasi pacchetto upstream dipende da un pacchetto di livello inferiore viene automaticamente disinstallato.

  + Per l'integrazione di Java, rimuovere **mssql-server-extensibility-java**

Comandi per la rimozione dei pacchetti vengono visualizzati nella tabella seguente.

| Piattaforma  | Comandi di rimozione pacchetto | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove msssql-server-extensibility-java`|

### <a name="3-proceed-with-ctp-30-install"></a>3. Procedere con l'installazione di CTP 3.0

Installare il massimo livello di pacchetto seguendo le istruzioni riportate in questo articolo per il sistema operativo.

Per ogni set di specifiche del sistema operativo di istruzioni di installazione *massimo livello di pacchetto* può essere **esempio 1: installazione completa** per il set completo di pacchetti, o **esempio 2 - installazione minima**  per il minor numero di pacchetti necessari per un'installazione valida.

1. Eseguire i comandi di installazione utilizzando la sintassi e i gestori di pacchetti per la distribuzione di Linux: 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>Prerequisiti

+ La versione di Linux deve essere [supportati da SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), ma non include il motore Docker. Le versioni supportate sono:

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ È necessario uno strumento per l'esecuzione di comandi T-SQL. Un editor di query è necessario per la convalida e configurazione di post-installazione. È consigliabile [Studio di Azure Data](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), un download gratuito che viene eseguito in Linux.

## <a name="package-list"></a>Elenco dei pacchetti

In un dispositivo connesso a internet, i pacchetti vengono scaricati e installati indipendentemente dal motore di database mediante il programma di installazione del pacchetto per ogni sistema operativo. La tabella seguente descrive tutti i pacchetti disponibili.

| Nome pacchetto | Si applica a | Descrizione |
|--------------|----------|-------------|
|mssql-server-extensibility  | Tutte le lingue | Framework di estendibilità utilizzato per eseguire codice Java. |
|mssql-server-extensibility-java | Java | Estensione di Java per il caricamento di un ambiente di esecuzione di Java. Non esistono altre librerie o pacchetti per Java. |

<a name="RHEL"></a>

## <a name="install-language-extensions"></a>Installare le estensioni del linguaggio

È possibile installare le estensioni del linguaggio e Java su Linux tramite l'installazione **mssql-server-extensibility-java**. Quando si installa **mssql-server-extensibility-java**, il pacchetto viene installato automaticamente JRE 8 se non è già installato. Aggiungerà anche il percorso JVM per una variabile di ambiente denominata riportato.

> [!Note]
> In un server connesso a internet, le dipendenze dei pacchetti vengono scaricate e installate come parte dell'installazione del pacchetto principale. Se il server non è connesso a internet, vedere altre informazioni, vedere la [programma di installazione offline](#offline-install).

### <a name="redhat-install-command"></a>Comando di installazione di RedHat

È possibile installare le estensioni del linguaggio per Java su RedHat usando il comando seguente.

> [!Tip]
> Se possibile, eseguire `yum clean all` per aggiornare i pacchetti nel sistema prima dell'installazione.

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Comando di installazione di Ubuntu

È possibile installare le estensioni del linguaggio per Java in Ubuntu utilizzando il comando seguente.

> [!Tip]
> Se possibile, eseguire `apt-get update` per aggiornare i pacchetti nel sistema prima dell'installazione. Inoltre, alcune immagini docker di Ubuntu potrebbero non avere l'opzione di apt trasporto https. Per installarlo, usare `apt-get install apt-transport-https`.

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>Comando di installazione SUSE

È possibile installare le estensioni del linguaggio per Java in SUSE con il comando seguente.

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>Configurazione di post-installazione (obbligatorio)

1. Concedere le autorizzazioni in Linux

    Non è necessario eseguire questo passaggio se si utilizzano librerie esterne. Il modo consigliato di utilizza librerie esterne. Per informazioni sulla creazione di una libreria esterna dal file con estensione jar, vedere [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)

    Se non si Usa librerie esterne, è necessario fornire a SQL Server le autorizzazioni per eseguire le classi Java in un file jar.

    Per concedono autorizzazioni di lettura ed eseguire l'accesso a un file con estensione jar, eseguire il comando seguente **chmod** comando sul file con estensione jar. È consigliabile inserire sempre i file di classe in un file jar quando si lavora con SQL Server. Per informazioni sulla creazione di un file jar, vedere [come creare un file con estensione jar](https://docs.microsoft.com/sql/language-extensions/how-to/create-a-java-jar-file-from-class-files).

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    È inoltre necessario concedere le autorizzazioni mssql_satellite il file jar in lettura/esecuzione.

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    Configurazione aggiuntiva viene eseguito principalmente tramita il [lo strumento mssql-conf](sql-server-linux-configure-mssql-conf.md).

2. Aggiungere l'account utente mssql utilizzato per eseguire il servizio SQL Server. È obbligatorio se è stato ancora eseguito il programma di installazione in precedenza.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. Abilitare l'accesso alla rete in uscita. Accesso alla rete in uscita è disabilitata per impostazione predefinita. Per abilitare le richieste in uscita, impostare "outboundnetworkaccess" proprietà Boolean utilizzando lo strumento mssql-conf. Per altre informazioni, vedere [configurare SQL Server in Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. Riavviare il servizio Launchpad di SQL Server e l'istanza del motore di database per leggere i valori aggiornati dal file INI. Ricorda di un messaggio di riavvio ogni volta che viene modificata un'impostazione di estendibilità.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. Abilitare l'esecuzione dello script esterno usando Azure Data Studio o un altro strumento come SQL Server Management Studio (solo Windows) che esegue Transact-SQL.

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. Riavviare il `mssql-launchpadd` service nuovamente.

7. Per ogni database che si desidera usare le estensioni del linguaggio in, è necessario registrare il linguaggio esterno con [linguaggio esterno creare](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql).

## <a name="verify-installation"></a>Verificare l'installazione

Integrazione delle funzionalità Java non include le librerie, ma è possibile eseguire `grep -r JRE_HOME /etc` per confermare la creazione della variabile di ambiente JAVA_HOME.

Per convalidare l'installazione, eseguire uno script T-SQL che esegue un sistema di stored procedure chiamata a Java. È necessario uno strumento di query per questa attività. Azure Data Studio è una scelta ottimale. Altri utilizzati di frequente strumenti come SQL Server Management Studio o PowerShell sono solo Windows. Se si dispone di un computer Windows con questi strumenti, usarlo per connettersi all'installazione di Linux del motore di database.

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-language-extensions"></a>Installazione completa di SQL Server e le estensioni del linguaggio

È possibile installare e configurare il motore di database e le estensioni del linguaggio in una procedura mediante l'aggiunta di parametri in un comando che installa il motore di database e i pacchetti Java.

1. Fornire una riga di comando che include il motore di database, oltre a funzionalità di estensione del linguaggio.

  È possibile aggiungere estensibilità per un motore di database installare Java.

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

3. Accettare i contratti di licenza e completare la configurazione di post-installazione. Usare la **mssql-conf** dello strumento per questa attività.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  Verrà richiesto di accettare il contratto di licenza per il motore di database, scegliere un'edizione e impostare la password dell'amministratore. 

4. Riavviare il servizio, se viene richiesto di farlo.

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>Installazione automatica

Usando il [installazione automatica](https://docs.microsoft.com/sql/linux/sql-server-linux-setup#unattended) per il motore di Database, aggiungere i pacchetti per mssql-server-extensibility-java.

<a name="offline-install"></a>


## <a name="offline-installation"></a>Installazione offline

Seguire le [installazione Offline](sql-server-linux-setup.md#offline) istruzioni per la procedura di installazione dei pacchetti. Trovare il sito di download e quindi scaricare pacchetti specifici usando l'elenco dei pacchetti riportato di seguito.

> [!Tip]
> Molti degli strumenti di gestione pacchetti forniscono comandi utili per determinano le dipendenze dei pacchetti. Per yum, usare `sudo yum deplist [package]`. Per Ubuntu, utilizzare `sudo apt-get install --reinstall --download-only [package name]` seguita da `dpkg -I [package name].deb`.

#### <a name="download-site"></a>Sito di download

È possibile scaricare i pacchetti da [ https://packages.microsoft.com/ ](https://packages.microsoft.com/). Tutti i pacchetti per Java vengono collocati con pacchetto del motore di database. 

#### <a name="redhat7-paths"></a>Percorsi di RedHat/7

|||
|--|----|
| pacchetti MSSQL/extensibility-java | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |

#### <a name="ubuntu1604-paths"></a>Percorsi/Ubuntu 16.04

|||
|--|----|
| pacchetti MSSQL/extensibility-java | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |

#### <a name="suse12-paths"></a>Percorsi SUSE 12

|||
|--|----|
| pacchetti MSSQL/extensibility-java | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |

#### <a name="package-list"></a>Elenco dei pacchetti

A seconda le estensioni che si desidera utilizzare, scaricare i pacchetti necessari per una lingua specifica. I nomi file esatti includono informazioni sulla piattaforma nel suffisso, ma i nomi di file riportato di seguito devono essere sufficientemente vicine per determinare i file da ottenere.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations-in-ctp-releases"></a>Limitazioni nelle versioni CTP

L'estendibilità le estensioni del linguaggio e Java in Linux è ancora in fase di sviluppo. Le funzionalità seguenti non sono ancora abilitate nella versione di anteprima.

+ L'autenticazione implicita non è attualmente disponibile in Linux a questo punto, il che significa che non è possibile connettersi al server da Java in corso per accedere a dati o altre risorse.


### <a name="resource-governance"></a>Governance delle risorse

È disponibile la parità tra Linux e Windows per [governance delle risorse](../t-sql/statements/create-external-resource-pool-transact-sql.md) per il pool di risorse esterne, ma le statistiche per [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) dispone attualmente unità di misura diversa in Linux. Le unità vengono allineati in una versione CTP successiva.
 
| Nome colonna   | Descrizione | Valore in Linux | 
|---------------|--------------|---------------|
|peak_memory_kb | La quantità massima di memoria utilizzata per il pool di risorse. | In Linux, questa statistica è originata dal sottosistema di memoria Cgroup, dove il valore è memory.max_usage_in_bytes |
|write_io_count | Totale scrittura generati dalla reimpostazione delle statistiche di Resource Governor. | In Linux, questa statistica è originata dal sottosistema di blkio Cgroup, dove il valore della riga di scrittura è blkio.throttle.io_serviced | 
|read_io_count | Il totale di lettura generati dalla reimpostazione delle statistiche di Resource Governor. | In Linux, questa statistica è originata dal sottosistema di blkio Cgroup, in cui valore della riga di lettura è blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | CPU utente kernel tempo totale espresso in millisecondi, reimpostazione delle statistiche di Resource Governor. | In Linux, questa statistica è originata dal sottosistema di cpuacct Cgroup, dove il valore nella riga dell'utente è cpuacct.stat |  
|total_cpu_user_ms | Tempo cumulativo della CPU di un utente espresso in millisecondi, reimpostazione delle statistiche di Resource Governor.| In Linux, questa statistica è originata dal sottosistema di cpuacct Cgroup, dove il valore per il valore di riga del sistema è cpuacct.stat | 
|active_processes_count | Il numero di processi esterni in esecuzione al momento della richiesta.| In Linux, questa statistica è originata dal sottosistema dei PID GGroups, dove il valore è pids.current | 

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori Java possono iniziare a usare alcuni semplici esempi e informazioni di base del funzionamento di Java con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Espressioni regolari con Java](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)