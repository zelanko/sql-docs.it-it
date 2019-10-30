---
title: Novità di SQL Server 2017 in Linux
description: Questo articolo mette in evidenza le novità di SQL Server 2017 in Linux.
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 6874c34c70b562ef726bda5abbda2aebe615cc08
ms.sourcegitcommit: bb56808dd81890df4f45636b600aaf3269c374f2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/24/2019
ms.locfileid: "72890549"
---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>Novità di SQL Server 2017 in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo descrive le funzionalità e i servizi principali disponibili per SQL Server 2017 in esecuzione in Linux.

> [!NOTE]
> Oltre alle funzionalità descritte in questo articolo, vengono rilasciati a intervalli regolari aggiornamenti cumulativi che mettono a disposizione numerosi miglioramenti e diverse correzioni. Per informazioni dettagliate sulla versione più recente degli aggiornamenti cumulativi, vedere [https://aka.ms/sql2017cu](https://aka.ms/sql2017cu). Per il download dei pacchetti e per informazioni sui problemi noti, vedere le [Note sulla versione ](sql-server-linux-release-notes.md).

## <a name="sql-server-database-engine"></a>Motore di database di SQL Server

- Abilitazione delle funzionalità di base del motore di database di SQL Server.
- Supporto dei percorsi Linux nativi.
- Supporto di IPV6.
- Supporto dei file di database in NFS.
- Abilitazione della crittografia [Transport Layer Security](sql-server-linux-encrypted-connections.md) (TLS).
- Abilitazione dell'[autenticazione di Active Directory](sql-server-linux-active-directory-authentication.md).
- [Funzionalità Gruppi di disponibilità](sql-server-linux-availability-group-overview.md) per garantire la disponibilità elevata.
- Supporto della [ricerca full-text](sql-server-linux-setup-full-text-search.md).

## <a name="sql-server-agent"></a>SQL Server Agent

- Supporto di [SQL Server Agent](sql-server-linux-setup-sql-agent.md) per le attività seguenti:
  - [Processi Transact-SQL](sql-server-linux-run-sql-server-agent-job.md)
  - [Posta elettronica database](sql-server-linux-db-mail-sql-agent.md)
  - [Log shipping](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- Possibilità di eseguire pacchetti SSIS in Linux. Per altre informazioni, vedere [Configurare SQL Server Integration Services in Linux con ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="other-improvements"></a>Altri miglioramenti

- Strumento di configurazione da riga di comando [mssql-conf](sql-server-linux-configure-mssql-conf.md).
- Supporto dell'installazione automatica con [variabili di ambiente](sql-server-linux-configure-environment-variables.md).
- [Estensione mssql-server di Visual Studio Code](sql-server-linux-develop-use-vscode.md) multipiattaforma.
- Generatore di script multipiattaforma, [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md).
- Strumento di monitoraggio DMV multipiattaforma, [DBFS](https://github.com/Microsoft/dbfs).

## <a name="next-steps"></a>Passaggi successivi

Per installare SQL Server in Linux, usare una delle esercitazioni seguenti:

- [Eseguire l'installazione in Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Eseguire l'installazione in SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Eseguire l'installazione in Ubuntu](quickstart-install-connect-ubuntu.md)
- [Esecuzione in Docker](quickstart-install-connect-docker.md)
- [Eseguire il provisioning di una macchina virtuale SQL in Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

Per le risposte alle domande frequenti, vedere [Domande frequenti su SQL Server in Linux](sql-server-linux-faq.md). Per informazioni su altri miglioramenti introdotti in SQL Server 2017, vedere [Novità di SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
