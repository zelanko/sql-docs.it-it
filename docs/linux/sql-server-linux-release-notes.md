---
title: Note sulla versione di SQL Server 2017 in Linux | Microsoft Docs
description: Questo articolo contiene le note sulla versione e funzionalità supportate per SQL Server 2017 in esecuzione su Linux. Note sulla versione sono incluse per la versione più recente e versioni precedenti.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 06/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: da7d92fd1fa15deb83dbca9a1710b967d660b99f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705150"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Note sulla versione di SQL Server 2017 in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Le note sulla versione seguenti si applicano a [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] in esecuzione su Linux. Questo articolo viene suddiviso in sezioni per ogni versione. La versione GA è supportability dettagliate ed elencati problemi noti. Ogni aggiornamento cumulativo (CU) o release generali di distribuzione (GDR) è disponibile un collegamento a un articolo di supporto che descrive il modifiche CU nonché collegamenti a Linux download del pacchetto.

> [!TIP]
> Queste note sulla versione sono specifici per [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] rilascia. Per altre informazioni sulla nuova [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], vedere [note sulla versione di anteprima di SQL Server 2019 in Linux](sql-server-linux-release-notes-2019.md?view=sql-server-ver15).

## <a name="supported-platforms"></a>Piattaforme supportate

| Piattaforma | File system | Guida all'installazione |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5 o 7.6 Server | XFS o EXT4 | [Guida all'installazione](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS o EXT4 | [Guida all'installazione](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS o EXT4 | [Guida all'installazione](quickstart-install-connect-ubuntu.md) | 
| Motore docker 1.8 + per Windows, Mac o Linux | N/D | [Guida all'installazione](quickstart-install-connect-docker.md) | 

> [!TIP]
> Per altre informazioni, vedere la [requisiti di sistema](sql-server-linux-setup.md#system) per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux. Per i criteri di supporto più recenti per [!INCLUDE[ssSQL17](../includes/sssql17-md.md)], vedere la [dei criteri di supporto tecnico per Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Strumenti

Client la maggior parte degli strumenti destinati [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] possono fare facilmente riferimento [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in esecuzione su Linux. Alcuni strumenti potrebbero avere un requisito di versione specifico per l'uso con Linux. Per un elenco completo delle [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] degli strumenti, vedere [SQL strumenti e utilità per SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Cronologia versioni

La tabella seguente elenca la cronologia di rilascio per [!INCLUDE[ssSQL17](../includes/sssql17-md.md)].

| Versione               | Version       | Data di rilascio |
|-----------------------|---------------|--------------|
| [CU15](#CU15)         | 14.0.3162.1   | 2019-05-23   |
| [CU14](#CU14)         | 14.0.3076.1   | 2019-03-25   |
| [CU13](#CU13)         | 14.0.3048.4   | 2018-12-18   |
| [CU12](#CU12)         | 14.0.3045.24  | 2018-10-24   |
| [CU11](#CU11)         | 14.0.3038.14  | 2018-09-20   |
| [CU10](#CU10)         | 14.0.3037.1   | 2018-08-27   |
| [CU9-GDR2](#CU9-GDR2) | 14.0.3035.2   | 2018-08-18   |
| [GDR2](#GDR2)         | 14.0.2002.14  | 2018-08-18   |
| [CU9](#CU9)           | 14.0.3030.27  | 2018-07-18   |
| [CU8](#CU8)           | 14.0.3029.16  | 2018-06-21   |
| [CU7](#CU7)           | 14.0.3026.27  | 2018-05-24   |
| [CU6](#CU6)           | 14.0.3025.34  | 2018-04-19   |
| [CU5](#CU5)           | 14.0.3023.8   | 2018-03-20   |
| [CU4](#CU4)           | 14.0.3022.28  | 2018-02-20   |
| [CU3](#CU3)           | 14.0.3015.40  | 2018-01-03   |
| [GDR1](#GDR1)         | 14.0.2000.63  | 2018-01-03   |
| [CU2](#CU2)           | 14.0.3008.27  | 2017-11-28   |
| [CU1](#CU1)           | 14.0.3006.16  | 2017-10-24   |
| [GA](#GA)             | 14.0.1000.169 | 2017-10-02   |

## <a id="cuinstall"></a> Come installare gli aggiornamenti

Se è stato configurato il repository CU (**mssql-server-2017**), si otterrà l'aggiornamento Cumulativo più recente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pacchetti quando si eseguono le nuove installazioni. Il repository CU è il valore predefinito per tutti i pacchetti di articoli di installazione per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux. Se è stato configurato il repository GDR (**mssql-server-2017-gdr**), si otterrà solo gli aggiornamenti critici della sicurezza rilasciati dal livello generale. Se è necessario il contenitore Docker CU o gli aggiornamenti GDR, vedere le immagini ufficiali per [Microsoft SQL Server in Linux per il motore Docker](https://hub.docker.com/r/microsoft/mssql-server). Per altre informazioni sulla configurazione del repository, vedere [configurare i repository per SQL Server in Linux](sql-server-linux-change-repo.md).

Se si sta aggiornando esistente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pacchetti, eseguire il comando di aggiornamento appropriato per ogni pacchetto ottenere l'aggiornamento Cumulativo più recente. Per istruzioni di aggiornamento specifico per ogni pacchetto, vedere le guide di installazione seguenti:

- [Installare il pacchetto di SQL Server](sql-server-linux-setup.md#upgrade)
- [Installare il pacchetto di ricerca Full-text](sql-server-linux-setup-full-text-search.md)
- [Installare SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Abilitare SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="CU15"></a> CU15 (maggio 2018)

Si tratta della versione 15 aggiornamento cumulativo (CU15) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3162.1. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/en-us/help/4498951 ](https://support.microsoft.com/en-us/help/4498951).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3162.1-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3162.1-1 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3162.1-1 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU14"></a> CU14 (marzo 2018)

Si tratta della versione 14 di aggiornamento cumulativo (CU14) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3076.1. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4484710 ](https://support.microsoft.com/help/4484710).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3076.1-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3076.1-2 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3076.1-2 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU13"></a> CU13 (Dec 2018)

Si tratta della versione 13 aggiornamento cumulativo (CU13) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3048.4. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4466404 ](https://support.microsoft.com/help/4466404).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3048.4-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3048.4-1 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3048.4-1 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a> CU12 (ottobre 2018)

Si tratta della versione 12 di aggiornamento cumulativo (CU12) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3045.24. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4464082 ](https://support.microsoft.com/help/4464082).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3045.24-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3045.24-1 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3045.24-1 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a> CU11 (settembre 2018)

Si tratta della versione 11 aggiornamento cumulativo (CU11) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3038.14. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4462262 ](https://support.microsoft.com/help/4462262).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3038.14-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3038.14-2 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3038.14-2 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a> CU10 (agosto 2018)

Si tratta della versione di aggiornamento cumulativo 10 (CU10) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3037.1. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4342123 ](https://support.microsoft.com/help/4342123).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3037.1-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3037.1-2 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3037.1-2 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a> CU9-GDR2 (agosto 2018)

Si tratta di un aggiornamento della sicurezza che include anche l'aggiornamento Cumulativo rilasciato in precedenza (CU9) per [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3035.2. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4293805 ](https://support.microsoft.com/help/4293805).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3035.2-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| Pacchetto RPM SLES | 14.0.3035.2-1 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3035.2-1 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a> GDR2 (agosto 2018)

Si tratta di un aggiornamento della sicurezza che include solo le correzioni di sicurezza GDR2 (e GDR1) per [!INCLUDE[ssSQL17](../includes/sssql17-md.md)].  Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.2002.14. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4293803 ](https://support.microsoft.com/help/4293803).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.2002.14-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.2002.14-1 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.2002.14-1 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a> CU9 (luglio 2018)

Si tratta della versione di aggiornamento cumulativo 9 (CU9) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3030.27. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4341265 ](https://support.microsoft.com/help/4341265).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3030.27-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3030.27-1 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3030.27-1 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a> CU8 (giugno 2018)

Si tratta della versione di aggiornamento cumulativo 8 (CU8) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3029.16. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4338363 ](https://support.microsoft.com/help/4338363).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3029.16-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3029.16-1 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3029.16-1 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a> CU7 (maggio 2018)

Si tratta della versione di aggiornamento cumulativo 7 (CU7) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3026.27. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4229789 ](https://support.microsoft.com/help/4229789).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3026.27-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3026.27-2 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3026.27-2 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a> CU6 (aprile 2018)

Si tratta della versione di aggiornamento cumulativo 6 (CU6) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3025.34. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3025.34-3 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3025.34-3 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3025.34-3 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5 (marzo 2018)

Si tratta della versione di aggiornamento cumulativo 5 (CU5) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3023.8. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4092643 ](https://support.microsoft.com/help/4092643).

### <a name="known-upgrade-issue"></a>Problema di aggiornamento noto

Quando esegue l'aggiornamento da una versione precedente a CU5, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non venga avviato con l'errore seguente:

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

Per risolvere questo errore, abilitare SQL Server Agent e riavviare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con i comandi seguenti:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3023.8-5 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3023.8-5 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3023.8-5 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a> CU4 (febbraio 2018)

Si tratta della versione di aggiornamento cumulativo 4 (CU4) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3022.28. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4056498 ](https://support.microsoft.com/help/4056498).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

> [!NOTE]
> A partire da CU4, SQL Server Agent non viene più installato come pacchetto separato. Viene installato con il pacchetto del motore e deve essere abilitata da utilizzare.

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3022.28-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3022.28-2 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3022.28-2 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a> GDR1 (gennaio 2018)

Si tratta di un aggiornamento della sicurezza che include solo il GDR1 le patch di protezione per [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.2000.63. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4057122 ](https://support.microsoft.com/help/4057122).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.2000.63-3 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.2000.63-3 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.2000.63-3 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a> CU3 (gennaio 2018)

Si tratta della versione di aggiornamento cumulativo 3 (CU3) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3015.40. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4052987 ](https://support.microsoft.com/help/4052987).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3015.40-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto RPM di SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3015.40-1 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto RPM di SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3015.40-1 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[Pacchetto Debian di SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (Nov 2017)

Si tratta della versione di aggiornamento cumulativo 2 (CU2) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3008.27. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/4052574 ](https://support.microsoft.com/help/4052574).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3008.27-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto RPM di SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3008.27-1 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto RPM di SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3008.27-1 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[Pacchetto Debian di SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (ottobre 2017)

Si tratta della versione di aggiornamento cumulativo 1 (CU1) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3006.16. Per informazioni sulle correzioni e miglioramenti in questa versione, vedere [ https://support.microsoft.com/help/KB4053439 ](https://support.microsoft.com/help/4038634).

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni manuali o offline del pacchetto, è possibile scaricare i pacchetti Debian e RPM con le informazioni nella tabella seguente:

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.3006.16-3 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto RPM di SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.3006.16-3 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto RPM di SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.3006.16-3 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[Pacchetto Debian di SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> Disponibilità generale (ottobre 2017)

Si tratta della versione GA (General Availability) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.1000.169.

### <a name="package-details"></a>Dettagli del pacchetto

Nella tabella seguente sono elencati i dettagli del pacchetto e percorsi di download per i pacchetti Debian e RPM. Si noti che non è necessario scaricare questi pacchetti direttamente se si usa la procedura nelle guide all'installazione seguente:

- [Installare il pacchetto di SQL Server](sql-server-linux-setup.md)
- [Installare il pacchetto di ricerca Full-text](sql-server-linux-setup-full-text-search.md)
- [Installare il pacchetto di SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [Installare SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| Pacchetto | Versione del pacchetto | Download |
|-----|-----|-----|
| Pacchetto di Red Hat RPM | 14.0.1000.169-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto RPM di SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto RPM SLES | 14.0.1000.169-2 | [pacchetto RPM motore MSSQL-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto RPM disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto RPM ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto RPM di SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian package | 14.0.1000.169-2 | [Pacchetto Debian motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Pacchetto Debian ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[Pacchetto Debian di SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> Servizi e funzionalità non supportate

Le funzionalità e i servizi seguenti non sono disponibili in Linux al momento della versione disponibile a livello generale. Il supporto di queste funzionalità verrà abilitato sempre più spesso nel corso del tempo.

| Area | Funzionalità non supportata o un servizio |
|-----|-----|
| **Motore di database** | Replica transazionale |
| &nbsp; | Replica di tipo merge |
| &nbsp; | Change Data Capture (vedere SQL Server Agent) |
| &nbsp; | Stretch database |
| &nbsp; | PolyBase |
| &nbsp; | Query distribuita con le connessioni 3rd-party |
| &nbsp; | Server collegati alle origini di dati diverso da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | Sistema (XP_CMDSHELL e così via) di stored procedure estesa |
| &nbsp; | Filetable FILESTREAM |
| &nbsp; | Gli assembly CLR con il EXTERNAL_ACCESS o UNSAFE autorizzazione impostata |
| &nbsp; | Estensione pool di buffer |
| **SQL Server Agent** |  Sottosistemi: CmdExec, PowerShell, Queue Reader, SSIS, SSAS, SSRS |
| &nbsp; | Avvisi |
| &nbsp; | Agente di lettura log |
| &nbsp; | Change Data Capture (CDC) |
| &nbsp; | Backup gestito |
| **Disponibilità elevata** | Mirroring del database  |
| **Sicurezza** | Extensible Key Management |
| &nbsp; | Autenticazione di Active Directory per i server collegati | 
| &nbsp; | Autenticazione di Active Directory per i gruppi di disponibilità (gruppi di disponibilità) | 
| &nbsp; | strumenti di terze parti AD 3rd (Centrify, Vintela, Powerbroker) | 
| **Services** | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |
| &nbsp; | Distributed Transaction Coordinator (DTC) |

## <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti con il rilascio GA (General Availability) di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] in Linux.

#### <a name="general"></a>Generale

- La lunghezza del nome host in cui [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è installato deve essere composto da 15 caratteri o meno. 

    - **Risoluzione**: Modificare il nome in /etc/hostname a un valore 15 caratteri lunghi o meno.

- Impostare manualmente con le versioni precedenti l'ora di sistema nel tempo determinerà [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per arrestare l'aggiornamento dell'ora di sistema interno all'interno di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

    - **Risoluzione**: Riavviare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

- Sono supportate solo le installazioni di istanza singola.

    - **Risoluzione**: Se si desidera avere più di un'istanza in un determinato host, è consigliabile usare le macchine virtuali o i contenitori Docker. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager non è possibile connettersi al [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux.

- La lingua predefinita del **sa** account di accesso è impostata sull'inglese.

    - **Risoluzione**: Modificare la lingua del **sa** account di accesso con il **ALTER LOGIN** istruzione.

#### <a name="databases"></a>Database

- Impossibile spostare il database master con l'utilità mssql-conf. Gli altri database di sistema possono essere spostati con mssql-conf.

- Quando si ripristina un database di cui è stato eseguito il backup su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Windows, è necessario utilizzare il **WITH MOVE** clausola nell'istruzione Transact-SQL.

- Non sono supportate le transazioni distribuite che richiedono il servizio Microsoft Distributed Transaction Coordinator in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in esecuzione su Linux. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sono supportati server collegati, a meno che non comportano il DTC. Per altre informazioni, vedere [le transazioni distribuite che richiedono il servizio Microsoft Distributed Transaction Coordinator non sono supportate in SQL Server in esecuzione su Linux](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/).

- Determinati algoritmi (pacchetti di crittografia) per Transport Layer Security (TLS) non funzionano correttamente con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux. Ciò comporta errori di connessione quando provano a connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], nonché i problemi per stabilire le connessioni tra repliche di gruppi di disponibilità elevata.

   - **Risoluzione**: Modificare il **mssql.conf** script di configurazione per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux per disabilitare i pacchetti di crittografia problematico, eseguendo le operazioni seguenti:

      1. Aggiungere quanto segue per /var/opt/mssql/mssql.conf.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Riavviare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con il comando seguente.

      ```bash
      sudo systemctl restart mssql-server
      ```

- [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] non è possibile ripristinare i database su Windows che utilizzano OLTP In memoria in [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] in Linux. Per ripristinare un [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] database che usa OLTP in memoria, eseguire prima l'aggiornamento dei database del [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] oppure [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] in Windows prima di spostarli a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] su Linux tramite backup e ripristino o scollegare o collegare.

- Autorizzazione utente **ADMINISTER BULK OPERATIONS** , in questo momento, non è supportato in Linux.

#### <a name="networking"></a>Rete

Le funzionalità che coinvolgono le connessioni TCP in uscita dal processo sqlservr, ad esempio i server collegati o gruppi di disponibilità, potrebbero non funzionare se vengono soddisfatte entrambe le condizioni seguenti:

1. Il server di destinazione viene specificato come un nome host e non un indirizzo IP.

1. L'istanza di origine ha disabilitato nel kernel di IPv6. Per verificare che se il sistema con IPv6 abilitato nel kernel, è necessario passare tutti i test seguenti:

   - `cat /proc/cmdline` consentirà di stampare la riga di comando di avvio del kernel corrente. L'output non deve contenere `ipv6.disable=1`.
   - Sys/proc / / net/ipv6 o della directory deve esistere.
   - Un programma C che chiama `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` dovrebbe avere esito positivo - syscall deve restituire un dominio di errore! = -1 e non avere esito negativo con EAFNOSUPPORT.

L'errore esatto varia a seconda della funzionalità. Per i server collegati, il problema può presentarsi come un errore di timeout di accesso. Per i gruppi di disponibilità, il `ALTER AVAILABILITY GROUP JOIN` DDL nel database secondario avrà esito negativo dopo 5 minuti con un errore di timeout di configurazione di download.

Per risolvere questo problema, effettuare una delle operazioni seguenti:

1. Usare gli indirizzi IP anziché i nomi host per specificare la destinazione della connessione TCP.

1. Abilitare IPv6 nel kernel rimuovendo `ipv6.disable=1` dalla riga di comando di avvio. Il modo per eseguire questa operazione dipende dalla distribuzione di Linux e il caricatore di avvio, ad esempio grub. Se si desidera IPv6 deve essere disabilitata, è comunque possibile disabilitarla impostando `net.ipv6.conf.all.disable_ipv6 = 1` nella `sysctl` configurazione (ad esempio `/etc/sysctl.conf`). Questo verrà comunque impedire l'introduzione di un indirizzo IPv6 di scheda di rete del sistema, ma consentire la funzionalità sqlservr.

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
Se si usa **Network File System (NFS)** condivisioni remote nell'ambiente di produzione, tenere presente i requisiti di supporto seguenti:

- Usare la versione NFS **4.2 o versione successiva**. Le versioni precedenti di NFS non supportano le funzionalità necessarie, ad esempio la creazione di file sparse, comune a moderno file System e fallocate.
- Individuare solo le **/var/opt/mssql** le directory di montaggio NFS. Altri file, ad esempio il [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] file binari del sistema, non sono supportati.
- Assicurarsi che i client NFS utilizzino l'opzione 'nolock' durante il montaggio di tale condivisione.

#### <a name="localization"></a>Localizzazione

- Se non le proprie impostazioni locali sono inglese (it_IT) durante l'installazione, è necessario utilizzare la codifica UTF-8 nella sessione/terminale bash. Se si usa la codifica ASCII, si potrebbe essere visualizzato un errore simile al seguente:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Se non è possibile utilizzare la codifica UTF-8, eseguire l'installazione utilizzando la variabile di ambiente MSSQL_LCID per specificare il linguaggio selezionato.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Quando si esegue il programma di installazione mssql-conf e l'esecuzione di un'installazione non in lingua inglese di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], errati caratteri estesi vengono visualizzati dopo il testo localizzato, "Configurazione di Server SQL...". O, per le installazioni di base non latini, la frase potrebbe non essere presente completamente. La frase manca deve visualizzare la stringa localizzata seguente: "Il PID di licenze è stato elaborato correttamente. La nuova edizione è [\<nome\> edition] ". Questa stringa è di output per a scopo esclusivamente informativo e quella successiva [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] si occuperanno questo aggiornamento cumulativo per tutte le lingue. Questa operazione non influenza la corretta installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in alcun modo. 

#### <a name="full-text-search"></a>Ricerca full-text

- Non tutti i filtri sono disponibili in questa versione, inclusi i filtri per i documenti di Office. Per un elenco dei filtri supportati, vedere [installazione di ricerca Full-Text di SQL Server in Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- Il **mssql-server-è** pacchetto non è supportato in SUSE in questa versione. È attualmente supportata in Ubuntu e Red Hat Enterprise Linux (RHEL).

- Con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in Linux CTP 2.1 aggiornare e versioni successive, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] i pacchetti possono usare le connessioni ODBC in Linux. Questa funzionalità è stata testata con la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e il driver ODBC MySQL, ma anche dovrebbe funzionare con qualsiasi driver ODBC Unicode che osserva la specifica ODBC. In fase di progettazione, è possibile fornire un DSN o una stringa di connessione per connettersi ai dati ODBC; è anche possibile usare l'autenticazione di Windows. Per altre informazioni, vedere la [post di blog annuncia il supporto ODBC in Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Le funzionalità seguenti non sono supportate in questa versione, quando si eseguono i pacchetti SSIS in Linux:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Database del catalogo
  - Esecuzione del pacchetto pianificato da SQL Agent
  - Autenticazione di Windows
  - Componenti di terze parti
  - Change Data Capture (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Scalabilità orizzontale
  - Azure Feature Pack per SSIS
  - Supporto di Hadoop e HDFS
  - Microsoft Connector for SAP BW

Per un elenco di componenti SSIS incorporati che non sono attualmente supportati o supportati con limitazioni, vedere [limitazioni e problemi noti per SSIS in Linux](sql-server-linux-ssis-known-issues.md#components).

Per altre informazioni su SSIS in Linux, vedere gli articoli seguenti:
-   [Blog post annuncia il supporto SSIS per Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Installare SQL Server Integration Services (SSIS) in Linux](sql-server-linux-setup-ssis.md)
-   [Estrarre, trasformare e caricare i dati in Linux con SSIS](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SQL Server Management Studio (SSMS)

Le limitazioni seguenti si applicano al [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] su Windows connessi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux.

- I piani di manutenzione non sono supportati.

- Gestione Data Warehouse di gestione e l'agente di raccolta dati in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] non sono supportati. 

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] I componenti dell'interfaccia utente con l'autenticazione di Windows o le opzioni del registro eventi di Windows non funzionano con Linux. È comunque possibile usare queste funzionalità con altre opzioni, ad esempio account di accesso SQL. 

- Impossibile modificare il numero di file di log da mantenere.

## <a name="next-steps"></a>Passaggi successivi

Per iniziare, vedere le guide introduttive seguenti:

- [Installare in Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installare in SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Eseguire l'installazione in Ubuntu](quickstart-install-connect-ubuntu.md)
- [Esecuzione in Docker](quickstart-install-connect-ubuntu.md)
- [Eseguire il provisioning di una macchina virtuale SQL in Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Esecuzione e connessione - Cloud](quickstart-install-connect-clouds.md)

Per le risposte alle domande più frequenti, vedere la [SQL Server in Linux FAQ](sql-server-linux-faq.md).
