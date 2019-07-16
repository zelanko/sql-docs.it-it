---
title: Guida all'installazione per SQL Server in Linux
titleSuffix: SQL Server
description: Installare, aggiornare e disinstallare SQL Server in Linux. Questo articolo descrive gli scenari online, offline e a quella automatico.
author: VanMSFT
ms.author: vanto
ms.date: 05/28/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.openlocfilehash: 7f4b2aa37b20cceaa3269527c95bfa97a2daa311
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032442"
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>Guida all'installazione per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo fornisce indicazioni per l'installazione, aggiornamento e disinstallazione di SQL Server 2017 e anteprima di SQL Server 2019 in Linux.

> [!TIP]
> Questa Guida coves diversi scenari di distribuzione. Se si sta cercando solo istruzioni dettagliate sull'installazione, passare a una delle guide introduttive:
> - [Guida introduttiva RHEL](quickstart-install-connect-red-hat.md)
> - [Guida introduttiva SLES](quickstart-install-connect-suse.md)
> - [Guida introduttiva di Ubuntu](quickstart-install-connect-ubuntu.md)
> - [Guida introduttiva a docker](quickstart-install-connect-docker.md)

Per le risposte alle domande più frequenti, vedere la [SQL Server in Linux FAQ](../linux/sql-server-linux-faq.md).

## <a id="supportedplatforms"></a> Piattaforme supportate

SQL Server 2017 è supportata in Ubuntu, SUSE Linux Enterprise Server (SLES) e Red Hat Enterprise Linux (RHEL). È anche supportato come immagine Docker, che può essere eseguito nel motore Docker in Linux o Docker per Windows/Mac.

| Piattaforma | Versioni supportate | Recupero
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3, 7.4, 7.5, 7.6 | [Ottenere RHEL 7.6](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [Ottenere SLES 12 SP2](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Ottenere Ubuntu 16.04](http://releases.ubuntu.com/xenial/)
| **Motore docker** | 1.8+ | [Ottieni Docker](https://www.docker.com/get-started)

Microsoft supporta anche la distribuzione e la gestione dei contenitori di SQL Server usando OpenShift e Kubernetes.

> [!NOTE]
> SQL Server viene testato e supportato in Linux per le distribuzioni elencate in precedenza. Se si sceglie di installare SQL Server in un sistema operativo non supportato, vedere la **criteri di supporto** sezione del [dei criteri di supporto tecnico per Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) per comprendere il supporto implicazioni.

## <a id="system"></a> Requisiti di sistema

SQL Server 2017 include i seguenti requisiti di sistema per Linux:

|||
|-----|-----|
| **Memoria** | 2 GB |
| **File system** | **XFS** oppure **EXT4** (altro file System, ad esempio **BTRFS**, non sono supportati) |
| **Spazio su disco** | 6 GB |
| **Velocità processore** | Almeno 2 GHz |
| **Memorie centrali del processore** | 2 core |
| **Tipo di processore** | compatibile con x64 solo |

Se si usa **Network File System (NFS)** condivisioni remote nell'ambiente di produzione, tenere presente i requisiti di supporto seguenti:

- Usare la versione NFS **4.2 o versione successiva**. Le versioni precedenti di NFS non supportano le funzionalità necessarie, ad esempio la creazione di file sparse, comune a moderno file System e fallocate.
- Individuare solo le **/var/opt/mssql** le directory di montaggio NFS. Altri file, ad esempio i file binari del sistema di SQL Server, non sono supportati.
- Assicurarsi che i client NFS utilizzino l'opzione 'nolock' durante il montaggio di tale condivisione.

## <a id="repositories"></a> Configurare i repository di origine

Quando si installa o si esegue l'aggiornamento di SQL Server, ottenere la versione più recente di SQL Server dal repository Microsoft configurato. Le guide introduttive usano l'aggiornamento di SQL Server 2017 Cumulative **CU** repository. Ma è invece possibile configurare il **GDR** repository o nella **anteprima (vNext)** repository. Per altre informazioni sul repository e come configurarle, vedere [configurare i repository per SQL Server in Linux](sql-server-linux-change-repo.md).

## <a id="platforms"></a> Installare SQL Server 2017

È possibile installare SQL Server 2017 in Linux dalla riga di comando. Per istruzioni dettagliate, vedere una delle guide introduttive seguenti:

- [Installare in Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installare in SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Eseguire l'installazione in Ubuntu](quickstart-install-connect-ubuntu.md)
- [Esecuzione in Docker](quickstart-install-connect-docker.md)
- [Eseguire il provisioning di una macchina virtuale SQL in Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

Dopo l'installazione, prendere in considerazione le modifiche di configurazione aggiuntive per ottenere prestazioni ottimali. Per altre informazioni, vedere [consigliate per le prestazioni e linee guida per la configurazione per SQL Server in Linux](sql-server-linux-performance-best-practices.md).

## <a id="sqlvnext"></a> Installare l'anteprima di SQL Server 2019

È possibile installare SQL Server 2019 anteprima in Linux con gli stessi collegamenti di Guida introduttiva nella sezione precedente. Tuttavia, è necessario registrare il **Preview (vNext)** repository anziché il **CU** repository. Le guide introduttive forniscono istruzioni su come eseguire questa operazione.  

## <a id="upgrade"></a> Aggiornare SQL Server

Per aggiornare il **mssql-server** alla versione più recente del pacchetto, usare uno dei seguenti comandi di base alla piattaforma:

| Piattaforma | Comandi di aggiornamento pacchetto |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

Questi comandi scaricano il pacchetto più recente e sostituire i file binari che si trova sotto `/opt/mssql/`. L'utente ha generato i database e i database di sistema non sono interessati da questa operazione.

> [!TIP]
> Se è primo [cambiare il repository configurato](sql-server-linux-change-repo.md), è possibile che il **aggiornare** comando per aggiornare la versione di SQL Server. Ciò avviene solo se il percorso di aggiornamento è supportato tra due repository.

## <a id="rollback"></a> Eseguire il rollback SQL Server

Per eseguire il rollback o il downgrade da SQL Server a una versione precedente, procedere come segue:

1. Identificare il numero di versione per il pacchetto di SQL Server che si desidera effettuare il downgrade a. Per un elenco di numeri di pacchetto, vedere la [note sulla versione](../linux/sql-server-linux-release-notes.md).

1. Effettuare il downgrade a una versione precedente di SQL Server. Nei comandi seguenti, sostituire `<version_number>` con il numero di versione di SQL Server identificato nel passaggio uno.

   | Piattaforma | Comandi di aggiornamento pacchetto |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> È supportato solo per effettuare il downgrade a una versione all'interno della stessa versione principale, ad esempio SQL Server 2017.

## <a id="versioncheck"></a> Controllare la versione di SQL Server installata

Per verificare la versione corrente e l'edizione di SQL Server in Linux, usare la procedura seguente:

1. Se non è già installato, installare il [gli strumenti da riga di comando di SQL Server](sql-server-linux-setup-tools.md).

1. Uso **sqlcmd** per eseguire il comando Transact-SQL che consente di visualizzare della versione di SQL Server e dell'edizione.

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a> Disinstallare SQL Server

Per rimuovere il **mssql-server** del pacchetto in Linux, usare uno dei seguenti comandi di base alla piattaforma:

| Piattaforma | Comandi di rimozione pacchetto |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

La rimozione del pacchetto non elimina i file di database generato. Se si desidera eliminare i file di database, usare il comando seguente:

```bash
sudo rm -rf /var/opt/mssql/
```

## <a id="unattended"></a> Installazione automatica

È possibile eseguire un'installazione automatica nel modo seguente:

- Attenersi alla procedura iniziale nel [guide introduttive](#platforms) per registrare il repository e installare SQL Server.
- Quando si esegue `mssql-conf setup`, impostare [variabili di ambiente](sql-server-linux-configure-environment-variables.md) e usare il `-n` (senza richiesta) opzione.

L'esempio seguente configura l'edizione Developer di SQL Server con il **MSSQL_PID** variabile di ambiente. L'attività accetta inoltre il contratto di licenza (**ACCEPT_EULA**) e imposta la password dell'utente dell'amministratore di sistema (**MSSQL_SA_PASSWORD**). Il `-n` parametro esegue l'installazione in cui vengono estratti i valori di configurazione dalle variabili di ambiente.

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

È anche possibile creare uno script che consente di eseguire altre azioni. Ad esempio, è possibile installare altri pacchetti di SQL Server.

Per uno script di esempio più dettagliato, vedere gli esempi seguenti:

- [Red Hat script di installazione automatica](sample-unattended-install-redhat.md)
- [SUSE script di installazione automatica](sample-unattended-install-suse.md)
- [Ubuntu script di installazione automatica](sample-unattended-install-ubuntu.md)

## <a id="offline"></a> Installazione offline

Se la macchina Linux non ha accesso al repository online usati nel [introduttive](#platforms), è possibile scaricare direttamente i file del pacchetto. Questi pacchetti si trovano nel repository Microsoft [ https://packages.microsoft.com ](https://packages.microsoft.com).

> [!TIP]
> Se è stato installato correttamente con i passaggi di avvio rapido, non occorre scaricare o installare manualmente i pacchetti di SQL Server. In questa sezione è solo per lo scenario offline.

1. **Scaricare il pacchetto di motore di database per la tua piattaforma**. Trovare collegamenti ai download dei pacchetti nella sezione dei dettagli del pacchetto di [note sulla versione](../linux/sql-server-linux-release-notes.md).

1. **Spostare il pacchetto scaricato nel computer Linux**. Se si usa un altro computer per scaricare i pacchetti, è un modo per spostare i pacchetti nel computer Linux con il **scp** comando.

1. **Installare il pacchetto di motore di database**. Usare uno dei seguenti comandi di base alla piattaforma. Sostituire il nome file del pacchetto in questo esempio con il nome esatto che è stato scaricato.

   | Piattaforma | Comando di installazione pacchetto |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > È anche possibile installare i pacchetti RPM (RHEL e SLES) con il `rpm -ivh` comando, ma i comandi nella tabella precedente installano automaticamente le dipendenze se approvato disponibile dal repository.

1. **Risolvere le dipendenze mancante**: Potrebbe essere mancante a questo punto le dipendenze. In caso contrario, è possibile ignorare questo passaggio. In Ubuntu, se si ha accesso ai repository approvati che contiene tali dipendenze, la soluzione più semplice consiste nell'utilizzare il `apt-get -f install` comando. Questo comando consente inoltre di completare l'installazione di SQL Server. Per controllare manualmente le dipendenze, usare i comandi seguenti:

   | Piattaforma | Comando Elenca le dipendenze |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   Dopo avere risolto le dipendenze mancanti, provare nuovamente a installare il pacchetto mssql-server.

1. **Completare l'installazione di SQL Server**. Uso **mssql-conf** per completare l'installazione di SQL Server:

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="licensing-and-pricing"></a>Gestione delle licenze e prezzi

Viene concesso in licenza SQL Server lo stesso per Linux e Windows. Per altre informazioni su SQL Server licenze e sui prezzi, vedere [licenza di SQL Server come](https://www.microsoft.com/sql-server/sql-server-2017-pricing).

## <a name="optional-sql-server-features"></a>Funzionalità facoltative di SQL Server

Dopo l'installazione, è anche possibile installare o abilitare le funzionalità facoltative di SQL Server.

- [Strumenti da riga di comando di SQL Server](sql-server-linux-setup-tools.md)
- [SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [Ricerca full-Text SQL Server](sql-server-linux-setup-full-text-search.md)
- [Machine Learning Services (R, Python)](sql-server-linux-setup-machine-learning.md)
- [SQL Server Integration Services](sql-server-linux-setup-ssis.md)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

> [!TIP]
> Per le risposte alle domande più frequenti, vedere la [SQL Server in Linux FAQ](sql-server-linux-faq.md).
