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
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032476"
---
# <a name="install-sql-server-agent-on-linux"></a>Installare SQL Server Agent in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

 [SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) esegue processi di SQL Server pianificati. A partire da SQL Server 2017 CU4, SQL Server Agent è incluso nel pacchetto **mssql-server** ed è disabilitato per impostazione predefinita. Per informazioni sulle funzionalità supportate per questa versione di SQL Server Agent, nonché per informazioni sulla versione, vedere le [note sulla versione](sql-server-linux-release-notes.md).

 Installare o abilitare SQL Server Agent:
- [Per le versioni 2017 CU4 e successive: abilitare SQL Server Agent](#EnableAgentAfterCU4)
- [Per le versioni 2017 CU3 e precedenti: installare SQL Server Agent](#InstallAgentBelowCU4)


## <a name="EnableAgentAfterCU4">Per le versioni 2017 CU4 e successive: abilitare SQL Server Agent</a>

 Per abilitare SQL Server Agent, seguire questa procedura.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> Se si esegue l'aggiornamento da 2017 CU3 o versione precedente e SQL Server Agent è installato, SQL Server Agent verrà abilitato automaticamente e i pacchetti di SQL Server Agent precedenti verranno disinstallati.  

## <a name="InstallAgentBelowCU4">Per le versioni 2017 CU3 e precedenti: installare SQL Server Agent</a>

> [!NOTE]
> Le istruzioni di installazione riportate di seguito si applicano a SQL Server versioni 2017 CU3 e precedenti. Prima di installare SQL Server Agent, [installare SQL Server](sql-server-linux-setup.md#platforms). In questo modo verranno configurate le chiavi e i repository usati durante l'installazione del pacchetto **mssql-server-agent**.

Installare SQL Server Agent per la piattaforma in uso:
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">Eseguire l'installazione in RHEL</a>

Seguire questa procedura per installare **mssql-server-agent** in Red Hat Enterprise Linux. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

Se il pacchetto **mssql-server-agent** è già installato, è possibile eseguire l'aggiornamento all'ultima versione con i comandi seguenti:

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

Se è necessaria un'installazione offline, individuare il download del pacchetto di SQL Server Agent nelle [Note sulla versione](sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](sql-server-linux-setup.md#offline).

### <a name="ubuntu">Eseguire l'installazione in Ubuntu</a>

Seguire questa procedura per installare **mssql-server-agent** in Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Se il pacchetto **mssql-server-agent** è già installato, è possibile eseguire l'aggiornamento all'ultima versione con i comandi seguenti:

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Se è necessaria un'installazione offline, individuare il download del pacchetto di SQL Server Agent nelle [Note sulla versione](sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](sql-server-linux-setup.md#offline).

### <a name="SLES">Eseguire l'installazione in SLES</a>

Seguire questa procedura per installare **mssql-server-agent** in SUSE Linux Enterprise Server. 

Installare **mssql-server-agent** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

Se il pacchetto **mssql-server-agent** è già installato, è possibile eseguire l'aggiornamento all'ultima versione con i comandi seguenti:

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

Se è necessaria un'installazione offline, individuare il download del pacchetto di SQL Server Agent nelle [Note sulla versione](sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](sql-server-linux-setup.md#offline).

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni su come usare SQL Server Agent per creare, pianificare ed eseguire processi, vedere [Eseguire un processo di SQL Server Agent in Linux](sql-server-linux-run-sql-server-agent-job.md).
