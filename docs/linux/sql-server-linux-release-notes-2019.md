---
title: Note sulla versione di SQL Server 2019 in Linux
description: Questo articolo contiene le note sulla versione e le funzionalità supportate per SQL Server 2019 in esecuzione in Linux. Sono incluse le note sulla versione per la versione più recente e per diverse versioni precedenti.
author: VanMSFT
ms.author: vanto
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: af3b6f82e3b76e2dd2b11403bccf4b3e0885912e
ms.sourcegitcommit: cbbb210c0315f9e2be2b9cd68db888ac53429814
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69890895"
---
# <a name="release-notes-for-sql-server-2019-on-linux"></a>Note sulla versione di SQL Server 2019 in Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

Le note sulla versione seguenti si applicano a SQL Server 2019 in esecuzione in Linux. Questo articolo è suddiviso in sezioni corrispondenti a ogni versione. Ogni versione ha un collegamento a un articolo del supporto che descrive le modifiche CU, oltre ai collegamenti ai download dei pacchetti Linux.

> [!TIP]
> Per informazioni sulle nuove funzionalità di Linux in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux).

## <a name="supported-platforms"></a>Piattaforme supportate

| Piattaforma | File system | Guida all'installazione |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5 o 7.6 Server | XFS o EXT4 | [Guida all'installazione](quickstart-install-connect-red-hat.md) | 
| SUSE Linux Enterprise Server v12 SP2 | XFS o EXT4 | [Guida all'installazione](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS o EXT4 | [Guida all'installazione](quickstart-install-connect-ubuntu.md) | 
| Docker Engine 1.8+ in Windows, Mac o Linux | N/D | [Guida all'installazione](quickstart-install-connect-docker.md) | 

> [!TIP]
> Per altre informazioni, vedere i [requisiti di sistema](sql-server-linux-setup.md#system) per SQL Server in Linux. Per i criteri di supporto tecnico più recenti per SQL Server 2017, vedere [Criteri di supporto tecnico per Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Strumenti

La maggior parte degli strumenti client esistenti per SQL Server può essere facilmente usata per SQL Server in esecuzione in Linux. Per usare in modo efficiente alcuni strumenti in Linux, potrebbe essere richiesta una versione specifica. Per un elenco completo di strumenti di SQL Server, vedere [Strumenti e utilità SQL per SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Cronologia delle versioni

La tabella seguente elenca la cronologia delle versioni di anteprima di SQL Server 2019.

| Versione                   | Versione       | Data di rilascio |
|---------------------------|---------------|--------------|
| [Release Candidate](#rc)  | 15.0.1900.25  | 21/08/2019    |
| [CTP 3.2](#CTP32)         | 15.0.1800.32  | 24/07/2019    |
| [CTP 3.1](#CTP31)         | 15.0.1700.37  | 26/06/2019    |
| [CTP 3.0](#CTP30)         | 15.0.1600.8   | 22/05/2019    |
| [CTP 2.5](#CTP25)         | 15.0.1500.28  | 24/04/2019    |
| [CTP 2.4](#CTP24)         | 15.0.1400.75  | 27/03/2019    |
| [CTP 2.3](#CTP23)         | 15.0.1300.359 | 01/03/2019    |
| [CTP 2.2](#CTP22)         | 15.0.1200.24  | 11/12/2018   |
| [CTP 2.1](#CTP21)         | 15.0.1100.94  | 06/11/2018   |
| [CTP 2.0](#CTP20)         | 15.0.1000.34  | 24/06/2018   |

## <a id="cuinstall"></a> Come installare gli aggiornamenti

Se è stato configurato il repository di anteprima (**mssql-server-preview**), quando si eseguono nuove installazioni, si otterranno i pacchetti di SQL Server CTP più recenti. Se sono necessarie le immagini del contenitore Docker, vedere le immagini ufficiali per [Microsoft SQL Server in Linux per il motore Docker](https://hub.docker.com/r/microsoft/mssql-server/). Per altre informazioni sulla configurazione del repository, vedere [Configurare i repository per SQL Server in Linux](sql-server-linux-change-repo.md).

Se si aggiornano pacchetti di SQL Server esistenti, eseguire il comando di aggiornamento appropriato per ogni pacchetto per ottenere l'aggiornamento cumulativo più recente. Per istruzioni dettagliate sull'aggiornamento per ogni pacchetto, vedere le guide all'installazione seguenti:

- [Installare il pacchetto di SQL Server](sql-server-linux-setup.md#upgrade)
- [Installare il pacchetto di ricerca full-text](sql-server-linux-setup-full-text-search.md)
- [Installare SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Installare il supporto per R e Python per Machine Learning Services dell'anteprima di SQL Server 2019 in Linux](sql-server-linux-setup-machine-learning.md)
- [Installare il pacchetto PolyBase](../relational-databases/polybase/polybase-linux-setup.md)
- [Abilitare SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="rc"></a> Release Candidate (agosto 2019)

Le sezioni seguenti elencano i percorsi dei pacchetti e i problemi noti per la versione finale candidata. Per altre informazioni sulle nuove funzionalità per Linux in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni dei pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 15.0.1900.25-1 | [Pacchetto RPM del motore](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1900.25-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| Pacchetto SLES RPM | 15.0.1900.25-1 | [Pacchetto RPM del motore mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1900.25-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| Pacchetto Ubuntu 16.04 Debian | 15.0.1900.25-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1900.25-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1900.25-1_amd64.deb)</br>[Pacchetto Debian di ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1900.25-1_amd64.deb)</br>[Pacchetto Debian di estendibilità](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1900.25-1_amd64.deb)</br>[Pacchetto Debian di estendibilità Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1900.25-1_amd64.deb)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1900.25-1_amd64.deb)|

## <a id="CTP32"></a> CTP 3.2 (luglio 2019)

Le sezioni seguenti elencano i percorsi dei pacchetti e i problemi noti per la versione CTP 3.2. Per altre informazioni sulle nuove funzionalità per Linux in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni dei pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 15.0.1800.32-1 | [Pacchetto RPM del motore](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| Pacchetto SLES RPM | 15.0.1800.32-1 | [Pacchetto RPM del motore mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| Pacchetto Ubuntu 16.04 Debian | 15.0.1800.32-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1800.32-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1800.32-1_amd64.deb)</br>[Pacchetto Debian di ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1800.32-1_amd64.deb)</br>[Pacchetto Debian di estendibilità](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1800.32-1_amd64.deb)</br>[Pacchetto Debian di estendibilità Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1800.32-1_amd64.deb)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1800.32-1_amd64.deb)|

## <a id="CTP31"></a> CTP 3.1 (giugno 2019)

Le sezioni seguenti elencano i percorsi dei pacchetti e i problemi noti per la versione CTP 3.1. Per altre informazioni sulle nuove funzionalità per Linux in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni dei pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 15.0.1700.37-2 | [Pacchetto RPM del motore](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| Pacchetto SLES RPM | 15.0.1700.37-2 | [Pacchetto RPM del motore mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| Pacchetto Ubuntu 16.04 Debian | 15.0.1700.37-2 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1700.37-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1700.37-2_amd64.deb)</br>[Pacchetto Debian di ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1700.37-2_amd64.deb)</br>[Pacchetto Debian di estendibilità](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1700.37-2_amd64.deb)</br>[Pacchetto Debian di estendibilità Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1700.37-2_amd64.deb)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1700.37-2_amd64.deb)|

## <a id="CTP30"></a> CTP 3.0 (maggio 2019)

Le sezioni seguenti elencano i percorsi dei pacchetti e i problemi noti per la versione CTP 3.0. Per altre informazioni sulle nuove funzionalità per Linux in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni dei pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 15.0.1600.8-1 | [Pacchetto RPM del motore](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Pacchetto SLES RPM | 15.0.1600.8-1 | [Pacchetto RPM del motore mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Pacchetto Ubuntu 16.04 Debian | 15.0.1600.8-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1600.8-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1600.8-1_amd64.deb)</br>[Pacchetto Debian di ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1600.8-1_amd64.deb)</br>[Pacchetto Debian di estendibilità](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1600.8-1_amd64.deb)</br>[Pacchetto Debian di estendibilità Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1600.8-1_amd64.deb)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1600.8-1_amd64.deb)|

### <a name="known-issues"></a>Problemi noti

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

Attualmente, MSDTC richiede che le transazioni non siano autenticate. Se ad esempio si usa un server collegato da SQL Server in Windows a SQL Server in Linux o si usa un'applicazione client Windows per avviare una transazione distribuita in SQL Server in Linux, è necessario che MSDTC nel server/client Windows usi l'opzione "Nessuna autenticazione".

## <a id="CTP25"></a> CTP 2.5 (aprile 2019)

Le sezioni seguenti elencano i percorsi dei pacchetti e i problemi noti per la versione CTP 2.5. Per altre informazioni sulle nuove funzionalità per Linux in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni dei pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 15.0.1500.28-1 | [Pacchetto RPM del motore](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Pacchetto SLES RPM | 15.0.1500.28-1 | [Pacchetto RPM del motore mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Pacchetto Ubuntu 16.04 Debian | 15.0.1500.28-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1500.28-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1500.28-1_amd64.deb)</br>[Pacchetto Debian di ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1500.28-1_amd64.deb)</br>[Pacchetto Debian di estendibilità](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1500.28-1_amd64.deb)</br>[Pacchetto Debian di estendibilità Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1500.28-1_amd64.deb)</br>[Pacchetto RPM PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1500.28-1_amd64.deb)|

### <a name="known-issues"></a>Problemi noti

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

Attualmente, MSDTC richiede che le transazioni non siano autenticate. Se ad esempio si usa un server collegato da SQL Server in Windows a SQL Server in Linux o si usa un'applicazione client Windows per avviare una transazione distribuita in SQL Server in Linux, è necessario che MSDTC nel server/client Windows usi l'opzione "Nessuna autenticazione".

## <a id="CTP24"></a> CTP 2.4 (marzo 2019)

Le sezioni seguenti elencano i percorsi dei pacchetti e i problemi noti per la versione CTP 2.4. Per altre informazioni sulle nuove funzionalità per Linux in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni dei pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 15.0.1400.75-2 | [Pacchetto RPM del motore](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Pacchetto SLES RPM | 15.0.1400.75-2 | [Pacchetto RPM del motore mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Pacchetto Ubuntu 16.04 Debian | 15.0.1400.75-2 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1400.75-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1400.75-2_amd64.deb)</br>[Pacchetto Debian di ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1400.75-2_amd64.deb)</br>[Pacchetto Debian di estendibilità](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1400.75-2_amd64.deb)</br>[Pacchetto Debian di estendibilità Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1400.75-2_amd64.deb)|

### <a name="known-issues"></a>Problemi noti

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

Attualmente, MSDTC richiede che le transazioni non siano autenticate. Se ad esempio si usa un server collegato da SQL Server in Windows a SQL Server in Linux o si usa un'applicazione client Windows per avviare una transazione distribuita in SQL Server in Linux, è necessario che MSDTC nel server/client Windows usi l'opzione "Nessuna autenticazione".

## <a id="CTP23"></a> CTP 2.3 (febbraio 2019)

Le sezioni seguenti elencano i percorsi dei pacchetti e i problemi noti per la versione CTP 2.3. Per altre informazioni sulle nuove funzionalità per Linux in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni dei pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 15.0.1300.359-1 | [Pacchetto RPM del motore](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Pacchetto SLES RPM | 15.0.1300.359-1 | [Pacchetto RPM del motore mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Pacchetto Ubuntu 16.04 Debian | 15.0.1300.359-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1300.359-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1300.359-1_amd64.deb)</br>[Pacchetto Debian di ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1300.359-1_amd64.deb)</br>[Pacchetto Debian di estendibilità](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1300.359-1_amd64.deb)</br>[Pacchetto Debian di estendibilità Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1300.359-1_amd64.deb)|

### <a name="known-issues"></a>Problemi noti

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

Attualmente, MSDTC richiede che le transazioni non siano autenticate. Se ad esempio si usa un server collegato da SQL Server in Windows a SQL Server in Linux o si usa un'applicazione client Windows per avviare una transazione distribuita in SQL Server in Linux, è necessario che MSDTC nel server/client Windows usi l'opzione "Nessuna autenticazione".

## <a id="CTP22"></a> CTP 2.2 (dicembre 2018)

Le sezioni seguenti elencano i percorsi dei pacchetti e i problemi noti per la versione CTP 2.2. Per altre informazioni sulle nuove funzionalità per Linux in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni dei pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 15.0.1200.24-2 | [Pacchetto RPM del motore](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Pacchetto SLES RPM | 15.0.1200.24-2 | [Pacchetto RPM del motore mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Pacchetto Ubuntu 16.04 Debian | 15.0.1200.24-2 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1200.24-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1200.24-2_amd64.deb)</br>[Pacchetto Debian di ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1200.24-2_amd64.deb)</br>[Pacchetto Debian di estendibilità](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1200.24-2_amd64.deb)</br>[Pacchetto Debian di estendibilità Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1200.24-2_amd64.deb)|

### <a name="known-issues"></a>Problemi noti

#### <a id="msdtc"></a> Microsoft Distributed Transaction Coordinator

Attualmente, MSDTC richiede che le transazioni non siano autenticate. Se ad esempio si usa un server collegato da SQL Server in Windows a SQL Server in Linux o si usa un'applicazione client Windows per avviare una transazione distribuita in SQL Server in Linux, è necessario che MSDTC nel server/client Windows usi l'opzione "Nessuna autenticazione".

## <a id="CTP21"></a> CTP 2.1 (novembre 2018)

Le sezioni seguenti elencano i percorsi dei pacchetti e i problemi noti per la versione CTP 2.1. Per altre informazioni sulle nuove funzionalità per Linux in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni dei pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 15.0.1100.94-1 | [Pacchetto RPM del motore](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Pacchetto SLES RPM | 15.0.1100.94-1 | [Pacchetto RPM del motore mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Pacchetto Ubuntu 16.04 Debian | 15.0.1100.94-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1100.94-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1100.94-1_amd64.deb)</br>[Pacchetto Debian di ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1100.94-1_amd64.deb)</br>[Pacchetto Debian di estendibilità](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1100.94-1_amd64.deb)</br>[Pacchetto Debian di estendibilità Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1100.94-1_amd64.deb)|

### <a name="known-issues"></a>Problemi noti

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft Distributed Transaction Coordinator

Attualmente, MSDTC richiede che le transazioni non siano autenticate. Se ad esempio si usa un server collegato da SQL Server in Windows a SQL Server in Linux o si usa un'applicazione client Windows per avviare una transazione distribuita in SQL Server in Linux, è necessario che MSDTC nel server/client Windows usi l'opzione "Nessuna autenticazione".

## <a id="CTP20"></a> CTP 2.0 (settembre 2018)

Le sezioni seguenti elencano i percorsi dei pacchetti e i problemi noti per la versione CTP 2.0. Per altre informazioni sulle nuove funzionalità per Linux in SQL Server 2019, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni dei pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 15.0.1000.34-2 | [Pacchetto RPM del motore](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Pacchetto SLES RPM | 15.0.1000.34-2 | [Pacchetto RPM del motore mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[Pacchetto RPM di ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Pacchetto RPM di estendibilità Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Pacchetto Ubuntu 16.04 Debian | 15.0.1000.34-2 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1000.34-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1000.34-2_amd64.deb)</br>[Pacchetto Debian di ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1000.34-2_amd64.deb)</br>[Pacchetto Debian di estendibilità](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1000.34-2_amd64.deb)</br>[Pacchetto Debian di estendibilità Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1000.34-2_amd64.deb)|

### <a name="known-issues"></a>Problemi noti

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft Distributed Transaction Coordinator

Attualmente, MSDTC richiede che le transazioni non siano autenticate. Se ad esempio si usa un server collegato da SQL Server in Windows a SQL Server in Linux o si usa un'applicazione client Windows per avviare una transazione distribuita in SQL Server in Linux, è necessario che MSDTC nel server/client Windows usi l'opzione "Nessuna autenticazione".

## <a name="next-steps"></a>Passaggi successivi

Per iniziare, vedere gli argomenti di avvio rapido seguenti:

- [Eseguire l'installazione in Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Eseguire l'installazione in SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Eseguire l'installazione in Ubuntu](quickstart-install-connect-ubuntu.md)
- [Esecuzione in Docker](quickstart-install-connect-ubuntu.md)
- [Eseguire il provisioning di una macchina virtuale SQL in Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Esecuzione e connessione - Cloud](quickstart-install-connect-clouds.md)

Per le risposte alle domande frequenti, vedere [Domande frequenti su SQL Server in Linux](sql-server-linux-faq.md).
