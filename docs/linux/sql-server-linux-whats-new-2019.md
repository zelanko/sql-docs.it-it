---
title: Novità di SQL Server 2019 in Linux
description: Questo articolo illustra le novità di SQL Server 2019 in Linux.
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5183efa51afd89ad82d0cdcb6448996429b81d28
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "72890552"
---
# <a name="whats-new-for-sql-server-2019-on-linux"></a>Novità di SQL Server 2019 in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo descrive le funzionalità e i servizi principali disponibili per SQL Server 2019 in esecuzione in Linux. Per il download dei pacchetti e per informazioni sui problemi noti, vedere le [Note sulla versione ](sql-server-linux-release-notes-2019.md?view=sql-server-linux-ver15).

## <a name="updates"></a>Aggiornamenti

Gli aggiornamenti sono stati eseguiti in SQL Server 2019 in Linux:

| Nuova funzionalità o aggiornamento | Dettagli |
|:-----|:-----|
|Supporto della replica |[Replica di SQL Server in Linux](sql-server-linux-replication.md)
|Supporto di Microsoft Distributed Transaction Coordinator (MSDTC) |[Come configurare MSDTC in Linux](sql-server-linux-configure-msdtc.md) |
|Supporto OpenLDAP per provider AD di terze parti |[Esercitazione: Usare l'autenticazione di Azure Active Directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md) |
|Machine Learning in Linux |[Configurare Machine Learning in Linux](sql-server-linux-setup-machine-learning.md) |
|Miglioramenti di `tempdb` | Per impostazione predefinita, una nuova installazione di SQL Server in Linux crea più file di dati `tempdb` in base al numero di core logici (con un massimo di 8 file di dati). Questo non vale per gli aggiornamenti sul posto di una versione principale o secondaria. Ogni file `tempdb` è di 8 MB, con un aumento automatico di 64 MB. Questo comportamento è simile all'installazione predefinita di SQL Server in Windows. |
| PolyBase in Linux | [Installare PolyBase](../relational-databases/polybase/polybase-linux-setup.md) in Linux per i connettori non Hadoop.<br/><br/>[Mapping dei tipi di PolyBase](../relational-databases/polybase/polybase-type-mapping.md). |
| Supporto di Change Data Capture (CDC) | Change Data Capture (CDC) è ora supportato in Linux per SQL Server 2019. |
| Registro Container Microsoft | Il [Registro Container Microsoft](https://www.ntweekly.com/2019/09/23/microsoft-container-registry-to-replace-docker-hub-for-new-images/) sostituisce ora Docker Hub per le nuove immagini di contenitori Microsoft ufficiali, incluso [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. |
| Contenitori non radice | In [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] è stata introdotta la possibilità di creare contenitori più sicuri avviando, per impostazione predefinita, il processo [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] come utente non radice. Per altri dettagli, vedere [Compilare ed eseguire contenitori di SQL Server come utente non radice](sql-server-linux-configure-docker.md#buildnonrootcontainer). |

## <a name="next-steps"></a>Passaggi successivi

Per installare SQL Server in Linux, usare una delle esercitazioni seguenti:

- [Eseguire l'installazione in Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md?view=sql-server-linux-ver15)
- [Eseguire l'installazione in SUSE Linux Enterprise Server](quickstart-install-connect-suse.md?view=sql-server-linux-ver15)
- [Eseguire l'installazione in Ubuntu](quickstart-install-connect-ubuntu.md?view=sql-server-linux-ver15)
- [Esecuzione in Docker](quickstart-install-connect-docker.md?view=sql-server-linux-ver15)
- [Eseguire il provisioning di una macchina virtuale SQL in Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

Per le risposte alle domande frequenti, vedere [Domande frequenti su SQL Server in Linux](sql-server-linux-faq.md). Per informazioni su altri miglioramenti introdotti in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
