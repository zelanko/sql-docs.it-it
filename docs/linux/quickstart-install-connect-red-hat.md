---
title: Introduzione a SQL Server su Red Hat Enterprise Linux
titleSuffix: SQL Server
description: Questa Guida introduttiva illustra come installare SQL Server 2017 o SQL Server 2019 in Red Hat Enterprise Linux e quindi creare ed eseguire query di un database con sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.custom: sql-linux, seodec18
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: dce4418dee10ff356d5c922350cd2fda29b44795
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277309"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>Avvio rapido: Installare SQL Server e creare un database in Red Hat

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

In questa Guida introduttiva, si installa SQL Server 2017 o SQL Server 2019 su Red Hat Enterprise Linux (RHEL). Quindi Connettiti **sqlcmd** per creare il primo database ed eseguire query.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

In questa Guida introduttiva, si installa SQL Server 2019 anteprima su Red Hat Enterprise Linux (RHEL) 7.3 +. Quindi Connettiti **sqlcmd** per creare il primo database ed eseguire query.

::: moniker-end

> [!TIP]
> Questa esercitazione richiede l'input dell'utente e una connessione a internet. Se è interessati al [automatica](sql-server-linux-setup.md#unattended) oppure [offline](sql-server-linux-setup.md#offline) procedure di installazione, vedere [informazioni aggiuntive sull'installazione per SQL Server in Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisiti

È necessario disporre di un computer con RHEL 7.3, 7.4, 7.5 o 7.6 **almeno 2 GB** di memoria.

Per installare Red Hat Enterprise Linux nel proprio computer, visitare [ https://access.redhat.com/products/red-hat-enterprise-linux/evaluation ](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation). È anche possibile creare macchine virtuali RHEL in Azure. Visualizzare [creare e gestire VM Linux con Azure CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)e usare `--image RHEL` nella chiamata a `az vm create`.

Se è stato precedentemente installato una versione CTP o RC di SQL Server 2017, è innanzitutto necessario rimuovere il repository precedente prima di seguire questi passaggi. Per altre informazioni, vedere [repository configurare Linux per SQL Server 2017 e 2019](sql-server-linux-change-repo.md).

Per altri requisiti di sistema, vedere [requisiti di sistema per SQL Server in Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>Installare SQL Server

Per configurare SQL Server in RHEL, eseguire i comandi seguenti in un terminale per installare il **mssql-server** pacchetto:

1. Scaricare il file di configurazione del repository di Microsoft SQL Server 2017 Red Hat:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!TIP]
   > Se si vuole provare 2019 di SQL Server, è necessario registrare invece le **Preview (2019)** repository. Usare il comando seguente per le installazioni di SQL Server 2019:
   >
   > ```bash
   > sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   > ```

2. Eseguire i comandi seguenti per installare SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. Dopo il completamento dell'installazione del pacchetto, eseguire **mssql-conf setup** e seguire le istruzioni per impostare la password account SA e scegliere l'edizione.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Le seguenti edizioni di SQL Server 2017 gratuitamente vengono concesso in licenza: Evaluation, Developer ed Express.

   > [!NOTE]
   > Assicurarsi di specificare una password complessa per l'account SA (caratteri di lunghezza 8 minimo, incluse le lettere maiuscole e lettere minuscole, cifre in base 10 e/o i simboli non alfanumerici).

4. Al termine della configurazione, verificare che il servizio sia in esecuzione:

   ```bash
   systemctl status mssql-server
   ```

5. Per consentire le connessioni remote, aprire la porta di SQL Server nel firewall in RHEL. La porta di SQL Server predefinita è TCP 1433. Se si usa **FirewallD** per firewall, è possibile usare i comandi seguenti:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

A questo punto, SQL Server è in esecuzione nel computer RHEL ed è pronto per l'uso.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>Installare SQL Server

Per configurare SQL Server in RHEL, eseguire i comandi seguenti in un terminale per installare il **mssql-server** pacchetto:

1. Scaricare l'anteprima di Microsoft SQL Server 2019 file di configurazione del repository di Red Hat:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   ```

2. Eseguire i comandi seguenti per installare SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. Dopo il completamento dell'installazione del pacchetto, eseguire **mssql-conf setup** e seguire le istruzioni per impostare la password account SA e scegliere l'edizione.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Assicurarsi di specificare una password complessa per l'account SA (caratteri di lunghezza 8 minimo, incluse le lettere maiuscole e lettere minuscole, cifre in base 10 e/o i simboli non alfanumerici).

4. Al termine della configurazione, verificare che il servizio sia in esecuzione:

   ```bash
   systemctl status mssql-server
   ```

5. Per consentire le connessioni remote, aprire la porta di SQL Server nel firewall in RHEL. La porta di SQL Server predefinita è TCP 1433. Se si usa **FirewallD** per firewall, è possibile usare i comandi seguenti:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

A questo punto, anteprima di SQL Server 2019 è in esecuzione nel computer RHEL e sia pronto per l'uso.

::: moniker-end

## <a id="tools"></a>Installare gli strumenti da riga di comando di SQL Server

Per creare un database, è necessario connettersi con uno strumento che è possibile eseguire istruzioni Transact-SQL in SQL Server. La procedura seguente installa gli strumenti da riga di comando di SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

1. Scaricare il file di configurazione del repository Microsoft Red Hat.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. Se si dispone di una versione precedente di **mssql-tools** installato, rimuovere eventuali pacchetti unixODBC meno recenti.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Eseguire i comandi seguenti per installare **mssql-tools** con il pacchetto di sviluppo unixODBC.

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. Per praticità, aggiungere `/opt/mssql-tools/bin/` per il **percorso** variabile di ambiente. Ciò consente di eseguire gli strumenti senza specificare il percorso completo. Eseguire i comandi seguenti per modificare la **percorso** per sessioni di accesso e le sessioni interattive/senza accesso:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
