---
title: Installare SQL Server Agent in Linux
description: Questo articolo descrive come installare SQL Server Agent in Linux.
author: VanMSFT
ms.author: vanto
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: c27a31a5e6b9ed771df82e942087d7be88270038
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032476"
---
# <a name="install-sql-server-agent-on-linux"></a>Installare SQL Server Agent in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

 Il [SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) esegue i processi pianificati di SQL Server. A partire da SQL Server 2017 CU4, SQL Server Agent è incluso con il **mssql-server** pacchetto ed è disabilitata per impostazione predefinita. Per informazioni sulle funzionalità supportate per questa versione di SQL Server Agent insieme a informazioni sulla versione, vedere la [note sulla versione](sql-server-linux-release-notes.md).

 Installa/Abilita SQL Server Agent:
- [Per le versioni 2017 CU4 e versioni successive, abilitare SQL Server Agent](#EnableAgentAfterCU4)
- [Per le versioni 2017 CU3 e versioni precedenti, installare SQL Server Agent](#InstallAgentBelowCU4)


## <a name="EnableAgentAfterCU4">Per le versioni 2017 CU4 e versioni successive, abilitare SQL Server Agent</a>

 Per abilitare SQL Server Agent, attenersi alla procedura seguente.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> Se si esegue l'aggiornamento da 2017 CU3 o sotto con installato l'agente di SQL Server Agent verrà abilitata automaticamente e quella precedente verranno disinstallati i pacchetti dell'agente.  

## <a name="InstallAgentBelowCU4">Per le versioni 2017 CU3 e versioni precedenti, installare SQL Server Agent</a>

> [!NOTE]
> Le istruzioni di installazione seguenti si applicano ad SQL Server versioni 2017 CU3 e versioni precedenti. Prima di installare SQL Server Agent, innanzitutto [installare SQL Server](sql-server-linux-setup.md#platforms). Ciò consente di configurare le chiavi e i repository che usano quando si installa il **mssql-server-agent** pacchetto.

Installare SQL Server Agent per la tua piattaforma:
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">Eseguire l'installazione in RHEL</a>

Usare la procedura seguente per installare il **mssql-server-agent** in Red Hat Enterprise Linux. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

Se hai già **mssql-server-agent** installato, è possibile aggiornare alla versione più recente con i comandi seguenti:

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

Se è necessaria un'installazione offline, individuare il download del pacchetto in SQL Server Agent il [note sulla versione](sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](sql-server-linux-setup.md#offline).

### <a name="ubuntu">Eseguire l'installazione in Ubuntu</a>

Usare la procedura seguente per installare il **mssql-server-agent** in Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Se hai già **mssql-server-agent** installato, è possibile aggiornare alla versione più recente con i comandi seguenti:

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Se è necessaria un'installazione offline, individuare il download del pacchetto in SQL Server Agent il [note sulla versione](sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](sql-server-linux-setup.md#offline).

### <a name="SLES">Eseguire l'installazione in SLES</a>

Usare la procedura seguente per installare il **mssql-server-agent** su SUSE Linux Enterprise Server. 

Installare **mssql-server-agent** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

Se hai già **mssql-server-agent** installato, è possibile aggiornare alla versione più recente con i comandi seguenti:

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

Se è necessaria un'installazione offline, individuare il download del pacchetto in SQL Server Agent il [note sulla versione](sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](sql-server-linux-setup.md#offline).

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni su come usare SQL Server Agent per creare, pianificare ed eseguire i processi, vedere [eseguire un processo di SQL Server Agent in Linux](sql-server-linux-run-sql-server-agent-job.md).
