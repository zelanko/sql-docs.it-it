---
title: Introduzione a SQL Server su SUSE Linux Enterprise Server
titleSuffix: SQL Server
description: Questa Guida introduttiva illustra come installare SQL Server 2017 o SQL Server 2019 su SUSE Linux Enterprise Server e quindi creare ed eseguire query di un database con sqlcmd.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.openlocfilehash: 19f74067db365fd9bdc867b97cef6ee5aa5162d8
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833253"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>Avvio rapido: Installare SQL Server e creare un database su SUSE Linux Enterprise Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

In questa Guida introduttiva, si installa SQL Server 2017 o SQL Server 2019 preview in SUSE Linux Enterprise Server (SLES) 12 SP2. Quindi Connettiti **sqlcmd** per creare il primo database ed eseguire query.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

In questa Guida introduttiva, anteprima di SQL Server 2019 è installare in SUSE Linux Enterprise Server (SLES) 12 SP2. Quindi Connettiti **sqlcmd** per creare il primo database ed eseguire query.

::: moniker-end

> [!TIP]
> Questa esercitazione richiede l'input dell'utente e una connessione a internet. Se è interessati al [automatica](sql-server-linux-setup.md#unattended) oppure [offline](sql-server-linux-setup.md#offline) procedure di installazione, vedere [informazioni aggiuntive sull'installazione per SQL Server in Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisiti

È necessario disporre di un SLES 12 SP2 computer con **almeno 2 GB** di memoria. Il file system deve essere **XFS** oppure **EXT4**. Altri file System, ad esempio **BTRFS**, non sono supportati.

Per installare SUSE Linux Enterprise Server nel proprio computer, visitare [ https://www.suse.com/products/server ](https://www.suse.com/products/server). È anche possibile creare macchine virtuali SLES in Azure. Visualizzare [creare e gestire VM Linux con Azure CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)e usare `--image SLES` nella chiamata a `az vm create`.

Se è stato precedentemente installato una versione CTP o RC di SQL Server 2017, è innanzitutto necessario rimuovere il repository precedente prima di seguire questi passaggi. Per altre informazioni, vedere [repository configurare Linux per SQL Server 2017 e 2019](sql-server-linux-change-repo.md).

> [!NOTE]
> A questo punto, il [sottosistema Windows per Linux](https://msdn.microsoft.com/commandline/wsl/about) per Windows 10 non è supportato come destinazione di installazione.

Per altri requisiti di sistema, vedere [requisiti di sistema per SQL Server in Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Installare SQL Server

Per configurare SQL Server in SLES, eseguire i comandi seguenti in un terminale per installare il **mssql-server** pacchetto:

1. Scaricare il file di configurazione del repository di Microsoft SQL Server 2017 SLES:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   ```

   > [!TIP]
   > Se si vuole provare 2019 di SQL Server, è necessario registrare invece le **Preview (2019)** repository. Usare il comando seguente per le installazioni di SQL Server 2019:
   >
   > ```bash
   > sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo
   > ```

2. Aggiornare i repository.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. Eseguire i comandi seguenti per installare SQL Server:

   ```bash
   sudo zypper install -y mssql-server
   ```

4. Dopo il completamento dell'installazione del pacchetto, eseguire **mssql-conf setup** e seguire le istruzioni per impostare la password account SA e scegliere l'edizione.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Le seguenti edizioni di SQL Server 2017 gratuitamente vengono concesso in licenza: Evaluation, Developer ed Express.

   > [!NOTE]
   > Assicurarsi di specificare una password complessa per l'account SA (caratteri di lunghezza 8 minimo, incluse le lettere maiuscole e lettere minuscole, cifre in base 10 e/o i simboli non alfanumerici).

5. Al termine della configurazione, verificare che il servizio sia in esecuzione:

   ```bash
   systemctl status mssql-server
   ```

6. Se si prevede di connettersi in remoto, si potrebbe essere necessario anche aprire la porta TCP di SQL Server (valore predefinito 1433) nel firewall. Se si usa il firewall di SuSE, è necessario modificare il **/etc/sysconfig/SuSEfirewall2** file di configurazione. Modificare il **FW_SERVICES_EXT_TCP** voce da includere il numero di porta di SQL Server.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

A questo punto, SQL Server è in esecuzione nel computer SLES ed è pronto per l'uso.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Installare SQL Server

Per configurare SQL Server in SLES, eseguire i comandi seguenti in un terminale per installare il **mssql-server** pacchetto:

1. Scaricare il file di configurazione del repository di Microsoft SQL Server 2019 anteprima SLES:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo
   ```

2. Aggiornare i repository.

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
3. Eseguire i comandi seguenti per installare SQL Server:

   ```bash
   sudo zypper install -y mssql-server
   ```

4. Dopo il completamento dell'installazione del pacchetto, eseguire **mssql-conf setup** e seguire le istruzioni per impostare la password account SA e scegliere l'edizione.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Assicurarsi di specificare una password complessa per l'account SA (caratteri di lunghezza 8 minimo, incluse le lettere maiuscole e lettere minuscole, cifre in base 10 e/o i simboli non alfanumerici).

5. Al termine della configurazione, verificare che il servizio sia in esecuzione:

   ```bash
   systemctl status mssql-server
   ```

6. Se si prevede di connettersi in remoto, si potrebbe essere necessario anche aprire la porta TCP di SQL Server (valore predefinito 1433) nel firewall. Se si usa il firewall di SuSE, è necessario modificare il **/etc/sysconfig/SuSEfirewall2** file di configurazione. Modificare il **FW_SERVICES_EXT_TCP** voce da includere il numero di porta di SQL Server.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

A questo punto, anteprima di SQL Server 2019 è in esecuzione nel computer SLES e sia pronto per l'uso.

::: moniker-end


## <a id="tools"></a>Installare gli strumenti da riga di comando di SQL Server

Per creare un database, è necessario connettersi con uno strumento che è possibile eseguire istruzioni Transact-SQL in SQL Server. La procedura seguente installa gli strumenti da riga di comando di SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

1. Aggiungere il repository di Microsoft SQL Server Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Installare **mssql-tools** con il pacchetto di sviluppo unixODBC.

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
   ```

1. Per praticità, aggiungere `/opt/mssql-tools/bin/` per il **percorso** variabile di ambiente. Ciò consente di eseguire gli strumenti senza specificare il percorso completo. Eseguire i comandi seguenti per modificare la **percorso** per sessioni di accesso e le sessioni interattive/senza accesso:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
