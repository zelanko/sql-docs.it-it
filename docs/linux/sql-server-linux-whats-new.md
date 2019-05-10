---
title: Novità di SQL Server 2017 in Linux | Microsoft Docs
description: Questo articolo vengono evidenziate nuove funzionalità per SQL Server 2017 in Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.openlocfilehash: d6f3d0b7fd60a39ce81a8464abdb6f2908f54239
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774755"
---
# <a name="whats-new-for-sql-server-on-linux"></a>Novità di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo descrive le funzionalità principali e i servizi disponibili per SQL Server 2017 in esecuzione su Linux.

È stato rilasciato l'anteprima di SQL Server 2019. Questo articolo non illustra le versioni di anteprima di SQL Server 2019. Per altre informazioni sull'anteprima di SQL Server 2019, vedere [nuove funzionalità di anteprima di SQL Server 2019 per Linux](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux).

> [!NOTE]
> Oltre a queste funzionalità in questo articolo, gli aggiornamenti cumulativi vengono rilasciati a intervalli regolari dopo il rilascio GA. che mettono a disposizione numerosi miglioramenti e diverse correzioni. Per informazioni sulla versione di aggiornamento Cumulativo più recente, vedere [ https://aka.ms/sql2017cu ](https://aka.ms/sql2017cu). Per il download del pacchetto e problemi noti, vedere la [note sulla versione](sql-server-linux-release-notes.md).

## <a name="sql-server-database-engine"></a>Motore di database di SQL Server

- Abilitare le funzionalità del motore di Database di SQL Server core.
- Supporto dei percorsi nativi di Linux.
- Supporto per IPv6.
- Supporto per file di database su NFS.
- Abilitata [Transport Layer Security](sql-server-linux-encrypted-connections.md) crittografia (TLS).
- Abilitata [autenticazione di Active Directory](sql-server-linux-active-directory-authentication.md).
- [La funzionalità gruppi di disponibilità](sql-server-linux-availability-group-overview.md) per la disponibilità elevata.
- [Ricerca full-text](sql-server-linux-setup-full-text-search.md) supportano.

## <a name="sql-server-agent"></a>SQL Server Agent

- Abilitata [SQL Server Agent](sql-server-linux-setup-sql-agent.md) il supporto per le attività seguenti:
  - [Processi di Transact-SQL](sql-server-linux-run-sql-server-agent-job.md)
  - [Posta elettronica database](sql-server-linux-db-mail-sql-agent.md)
  - [Log shipping](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- Possibilità di eseguire pacchetti SSIS in Linux. Per altre informazioni, vedere [configurare SQL Server Integration Services in Linux con ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="other-improvements"></a>Altri miglioramenti

- Strumento di configurazione della riga di comando [mssql-conf](sql-server-linux-configure-mssql-conf.md).
- Supporto di installazione automatica con [variabili di ambiente](sql-server-linux-configure-environment-variables.md).
- Lo sviluppo multipiattaforma [estensione mssql-server di Visual Studio Code](sql-server-linux-develop-use-vscode.md).
- Generatore di script multipiattaforma [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md).
- Monitoraggio vista a gestione dinamica (DMV) cross-platform [dello strumento DBFS](https://github.com/Microsoft/dbfs).

## <a name="next-steps"></a>Passaggi successivi

Per installare SQL Server in Linux, usare una delle esercitazioni seguenti:

- [Installare in Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installare in SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installazione in Ubuntu](quickstart-install-connect-ubuntu.md)
- [Esecuzione in Docker](quickstart-install-connect-docker.md)
- [Eseguire il provisioning di una macchina virtuale SQL in Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

Per informazioni su altri miglioramenti introdotti in SQL Server 2017, vedere [What ' s New in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

> [!TIP]
> Per le risposte alle domande più frequenti, vedere la [SQL Server in Linux FAQ](sql-server-linux-faq.md).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
