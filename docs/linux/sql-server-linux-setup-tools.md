---
title: Installare gli strumenti da riga di comando di SQL Server in Linux | Microsoft Docs
description: Questo articolo descrive come installare gli strumenti SQL Server in Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: 20b383929910bf24ef9dc89950f15815afdef3bd
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/25/2019
ms.locfileid: "56801755"
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Installare sqlcmd e bcp strumenti da riga di comando di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

La procedura seguente installa gli strumenti da riga di comando, i driver ODBC di Microsoft e le relative dipendenze. Il **mssql-tools** pacchetto contiene:

- **sqlcmd**: Utilità della riga di comando di query.
- **bcp**: Utilità di importazione / esportazione in blocco.

Installare gli strumenti per la piattaforma in uso:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

Questo articolo descrive come installare gli strumenti da riga di comando. Se si sta cercando esempi d'uso **sqlcmd** oppure **bcp**, vedere il [collegamenti](#next-steps) alla fine di questo argomento.

## <a name="a-idrhelainstall-tools-on-rhel-7"></a><a id="RHEL"><a/>Installare gli strumenti in RHEL 7

Usare la procedura seguente per installare il **mssql-tools** in Red Hat Enterprise Linux. 

1. Attivare la modalità utente con privilegi avanzati.

   ```bash
   sudo su
   ```

1. Scaricare il file di configurazione del repository Microsoft Red Hat.

   ```bash
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/msprod.repo
   ```

1. Esci dalla modalità utente con privilegi avanzati.

   ```bash
   exit
   ```

1. Se si dispone di una versione precedente di **mssql-tools** installato, rimuovere eventuali pacchetti unixODBC meno recenti.

   ```bash
   sudo yum remove mssql-tools unixODBC-utf16-devel
   ```

1. Eseguire i comandi seguenti per installare **mssql-tools** con il pacchetto di sviluppo unixODBC.

   ```bash
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Eseguire l'aggiornamento alla versione più recente di **mssql-tools** eseguire i comandi seguenti:
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **Facoltativo**: Aggiungere `/opt/mssql-tools/bin/` per il **percorso** variabile di ambiente in una shell bash.

   Per rendere **sqlcmd/bcp** accessibile da shell di bash per sessioni di accesso, modificare le **PATH** nel **~/.bash_profile** file con il comando seguente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Per rendere **sqlcmd/bcp** accessibile da shell di bash per le sessioni interattive/senza accesso, modificare il **PATH** nel **~/.bashrc** file con il comando seguente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="ubuntu"></a>Installare gli strumenti in Ubuntu 16.04

Usare la procedura seguente per installare il **mssql-tools** in Ubuntu. 

1. Importare le chiavi GPG repository pubblico.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registrare il repository Microsoft Ubuntu.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. Aggiornare l'elenco delle origini ed eseguire il comando di installazione con il pacchetto di sviluppo unixODBC.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > Eseguire l'aggiornamento alla versione più recente di **mssql-tools** eseguire i comandi seguenti:
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **Facoltativo**: Aggiungere `/opt/mssql-tools/bin/` per il **percorso** variabile di ambiente in una shell bash.

   Per rendere **sqlcmd/bcp** accessibile da shell di bash per sessioni di accesso, modificare le **PATH** nel **~/.bash_profile** file con il comando seguente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Per rendere **sqlcmd/bcp** accessibile da shell di bash per le sessioni interattive/senza accesso, modificare il **PATH** nel **~/.bashrc** file con il comando seguente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="SLES"></a>Installare gli strumenti in SLES 12

Usare la procedura seguente per installare il **mssql-tools** su SUSE Linux Enterprise Server. 

1. Aggiungere il repository di Microsoft SQL Server Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Installare **mssql-tools** con il pacchetto di sviluppo unixODBC.

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Eseguire l'aggiornamento alla versione più recente di **mssql-tools** eseguire i comandi seguenti:
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
   >   ```

1. **Facoltativo**: Aggiungere `/opt/mssql-tools/bin/` per il **percorso** variabile di ambiente in una shell bash.

   Per rendere **sqlcmd/bcp** accessibile da shell di bash per sessioni di accesso, modificare le **PATH** nel **~/.bash_profile** file con il comando seguente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Per rendere **sqlcmd/bcp** accessibile da shell di bash per le sessioni interattive/senza accesso, modificare il **PATH** nel **~/.bashrc** file con il comando seguente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="macos"></a> Installare gli strumenti in macOS

Un'anteprima dei **sqlcmd** e **bcp** è ora disponibile in macOS. Per altre informazioni, vedere la [annuncio](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/).

*Installare [Homebrew](https://brew.sh) se non è già presente:*

        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Per installare gli strumenti per Mac El Capitan e Sierra, usare i comandi seguenti:

```
# brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install mssql-tools
#for silent install: 
#HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=y brew install mssql-tools
```

## <a id="docker"></a> Docker

Gli strumenti da riga di comando di SQL Server sono inclusi nell'immagine Docker. Se si collega all'immagine con un prompt dei comandi interattiva, è possibile eseguire gli strumenti in locale.

## <a name="offline-installation"></a>Installazione offline

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

La tabella seguente fornisce il percorso per i pacchetti di strumenti più recenti:

| Pacchetto di strumenti | Versione | Scarica |
|-----|-----|-----|
| Pacchetto di strumenti di Red Hat RPM | 14.0.5.0-1 | [pacchetto RPM MSSQL-tools](https://packages.microsoft.com/rhel/7.3/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Pacchetto di strumenti di SLES RPM | 14.0.5.0-1 | [pacchetto RPM MSSQL-tools](https://packages.microsoft.com/sles/12/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian pacchetto degli strumenti | 14.0.5.0-1 | [pacchetto Debian MSSQL-tools](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |
| Ubuntu 16.10 Debian pacchetto degli strumenti | 14.0.5.0-1 | [pacchetto Debian MSSQL-tools](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |

Questi pacchetti dipendono **msodbcsql**, che deve essere installato per primo. Il **msodbcsql** quest'ultimo ha anche una dipendenza su uno **unixODBC-sviluppo per sistemi operativi** (RPM) oppure **unixodbc-dev** (Debian). Il percorso dei **msodbcsql** nella tabella seguente vengono elencati i pacchetti:

| msodbcsql pacchetto | Versione | Scarica |
|-----|-----|-----|
| Pacchetto di Red Hat RPM msodbcsql | 13.1.6.0-1 | [pacchetto RPM msodbcsql](https://packages.microsoft.com/rhel/7.3/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Pacchetto msodbcsql RPM SLES | 13.1.6.0-1 | [pacchetto RPM msodbcsql](https://packages.microsoft.com/sles/12/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian msodbcsql package | 13.1.6.0-1 | [pacchetto Debian msodbcsql](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |
| Ubuntu 16.10 Debian msodbcsql package | 13.1.6.0-1 | [pacchetto Debian msodbcsql](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |

Per installare manualmente questi pacchetti, procedere come segue:

1. **Spostare i pacchetti scaricati nel computer Linux**. Se si usa un altro computer per scaricare i pacchetti, è un modo per spostare i pacchetti nel computer Linux con il **scp** comando.

1. **Installare i pacchetti e**: Installare il **mssql-tools** e **msodbc** pacchetti. Se si verificano eventuali errori di dipendenza, è possibile ignorarli fino al passaggio successivo.

    | Piattaforma | Comandi di installazione pacchetto |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo yum localinstall mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | SLES | `sudo zypper install msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo zypper install mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_13.1.6.0-1_amd64.deb`<br/>`sudo dpkg -i mssql-tools_14.0.5.0-1_amd64.deb` |

1. **Risolvere le dipendenze mancante**: Potrebbe essere mancante a questo punto le dipendenze. In caso contrario, è possibile ignorare questo passaggio. In alcuni casi, è necessario individuare manualmente e installare queste dipendenze.

    Per i pacchetti RPM, è possibile controllare le dipendenze necessarie con i comandi seguenti:

    ```bash
    rpm -qpR msodbcsql-13.1.6.0-1.x86_64.rpm
    rpm -qpR mssql-tools-14.0.5.0-1.x86_64.rpm
    ```

    Per i pacchetti Debian, se si ha accesso ai repository approvati che contiene tali dipendenze, la soluzione più semplice consiste nell'usare la **apt-get** comando:

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > Questo comando viene completato l'installazione anche i pacchetti di SQL Server.

    Se questo non funziona per il pacchetto Debian, è possibile esaminare le dipendenze necessarie con i comandi seguenti:

    ```bash
    dpkg -I msodbcsql_13.1.6.0-1_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_14.0.5.0-1_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>Passaggi successivi

Per un esempio d'uso **sqlcmd** per connettersi a SQL Server e creare un database, vedere una delle guide introduttive seguenti:

- [Installare in Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installare in SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installazione in Ubuntu](quickstart-install-connect-ubuntu.md)
- [Esecuzione in Docker](quickstart-install-connect-ubuntu.md)

Per un esempio d'uso **bcp** per l'importazione ed esportazione bulk dei dati, vedere [copia Bulk di dati a SQL Server in Linux](sql-server-linux-migrate-bcp.md).
