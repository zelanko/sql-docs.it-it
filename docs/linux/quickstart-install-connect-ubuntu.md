---
title: Introduzione a SQL Server in Ubuntu
titleSuffix: SQL Server
description: Questa guida di avvio rapido illustra come installare SQL Server 2017 o SQL Server 2019 in Ubuntu e quindi come creare ed eseguire query su un database con sqlcmd.
author: VanMSFT
ms.author: vanto
ms.date: 05/28/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 23597e4937f279694d7e4286e5aec3d714b54afa
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67910458"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>Avvio rapido: Installare SQL Server e creare un database in Ubuntu
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]


<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

In questa guida di avvio rapido si installerà SQL Server 2017 o Anteprima di SQL Server 2019 in Ubuntu 16.04. Ci si connette quindi con **sqlcmd** per creare il primo database ed eseguire query.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

In questa guida di avvio rapido si installerà Anteprima di SQL Server 2019 in Ubuntu 16.04. Ci si connette quindi con **sqlcmd** per creare il primo database ed eseguire query.

::: moniker-end

> [!TIP]
> Questa esercitazione richiede l'input dell'utente e una connessione Internet. Se si è interessati alle procedure di installazione automatica o offline, vedere [Linee guida per l'installazione di SQL Server in Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisites

È necessario un computer Ubuntu 16.04 con **almeno 2 GB** di memoria.

Per installare Ubuntu 16,04 nel computer in uso, passare a [http://releases.ubuntu.com/xenial/](http://releases.ubuntu.com/xenial/). È anche possibile creare macchine virtuali Ubuntu in Azure. Vedere [Creare e gestire VM Linux con l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> Attualmente il [Sottosistema Windows per Linux](https://msdn.microsoft.com/commandline/wsl/about) per Windows 10 non è supportato come destinazione dell'installazione.

Per altri requisiti di sistema, vedere [Requisiti di sistema per SQL Server su Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Installare SQL Server

Per configurare SQL Server in Ubuntu e installare il pacchetto **mssql-server**, eseguire i comandi seguenti in un terminale.

1. Importare le chiavi GPG del repository pubblico:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registrare il repository Microsoft SQL Server per Ubuntu:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!TIP]
   > Se si vuole provare SQL Server 2019, occorre invece registrare il repository **Anteprima (2019)** . Usare il comando seguente per le installazioni di SQL Server 2019:
   >
   > ```bash
   > sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   > ```

3. Eseguire i comandi seguenti per installare SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. Al termine dell'installazione del pacchetto, eseguire **mssql-conf setup** e seguire le istruzioni per impostare la password dell'amministratore di sistema e scegliere l'edizione.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Le edizioni di SQL Server 2017 seguenti sono concesse in licenza gratuitamente: Evaluation, Developer ed Express.

   > [!NOTE]
   > Assicurarsi di specificare una password complessa per l'account dell'amministratore di sistema (lunghezza minima di 8 caratteri, con lettere sia maiuscole che minuscole, cifre in base 10 e/o simboli non alfanumerici).

5. Al termine della configurazione, verificare che il servizio sia in esecuzione:

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. Se si prevede di connettersi in modalità remota, potrebbe essere necessario aprire anche la porta TCP di SQL Server (per impostazione predefinita, la 1433) sul firewall.

A questo punto, SQL Server è in esecuzione nel computer Ubuntu ed è pronto per l'uso.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Installare SQL Server

Per configurare SQL Server in Ubuntu e installare il pacchetto **mssql-server**, eseguire i comandi seguenti in un terminale.

1. Importare le chiavi GPG del repository pubblico:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Registrare il repository Microsoft SQL Server per Ubuntu per Anteprima di SQL Server 2019:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   ```

3. Eseguire i comandi seguenti per installare SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. Al termine dell'installazione del pacchetto, eseguire **mssql-conf setup** e seguire le istruzioni per impostare la password dell'amministratore di sistema e scegliere l'edizione.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Assicurarsi di specificare una password complessa per l'account dell'amministratore di sistema (lunghezza minima di 8 caratteri, con lettere sia maiuscole che minuscole, cifre in base 10 e/o simboli non alfanumerici).

5. Al termine della configurazione, verificare che il servizio sia in esecuzione:

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. Se si prevede di connettersi in modalità remota, potrebbe essere necessario aprire anche la porta TCP di SQL Server (per impostazione predefinita, la 1433) sul firewall.

A questo punto, Anteprima di SQL Server 2019 è in esecuzione nel computer Ubuntu ed è pronto per l'uso.

::: moniker-end

## <a id="tools"></a>Installare gli strumenti da riga di comando di SQL Server

Per creare un database, è necessario connettersi con uno strumento in grado di eseguire istruzioni Transact-SQL nel server SQL. La procedura seguente installa gli strumenti da riga di comando di SQL Server [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

Seguire questa procedura per installare **mssql-tools** in Ubuntu. 

1. Importare le chiavi GPG del repository pubblico.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registrare il repository Microsoft per Ubuntu.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. Aggiornare l'elenco di origini ed eseguire il comando di installazione con il pacchetto per sviluppatori unixODBC.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > Per effettuare l'aggiornamento alla versione più recente di **mssql-tools**, eseguire i comandi seguenti:
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **Facoltativo**: aggiungere `/opt/mssql-tools/bin/` alla variabile di ambiente **PATH** in una shell Bash.

   Per rendere **sqlcmd/bcp** accessibile dalla shell Bash per le sessioni di accesso, modificare **PATH** nel file **~/.bash_profile** con il comando seguente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Per rendere **sqlcmd/bcp** accessibile dalla shell Bash per le sessioni interattive/non di accesso, modificare **PATH** nel file **~/.bashrc** con il comando seguente:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
