---
title: Note sulla versione per SQL Server 2017 in Linux
description: Questo articolo contiene le note sulla versione e le funzionalità supportate per SQL Server 2017 in esecuzione su Linux. Le note sulla versione sono incluse per la versione più recente e per diverse versioni precedenti.
author: VanMSFT
ms.author: vanto
ms.date: 06/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: 5b6fce0bdde7e320eea0371125a61627652de80d
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388406"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Note sulla versione per SQL Server 2017 in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Le note sulla versione seguenti si [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] applicano a in esecuzione su Linux. Questo articolo è suddiviso in sezioni per ogni versione. La versione GA include informazioni dettagliate sul supporto e sui problemi noti elencati. Ogni aggiornamento cumulativo (CU) o General Distribution Release (GDR) include un collegamento a un articolo del supporto che descrive le modifiche del CU e i collegamenti ai download del pacchetto Linux.

> [!TIP]
> Queste note sulla versione sono specifiche [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] per i rilasci. Per ulteriori informazioni sul nuovo [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], vedere [Note sulla versione per SQL Server anteprima 2019 in Linux](sql-server-linux-release-notes-2019.md?view=sql-server-ver15).

## <a name="supported-platforms"></a>Piattaforme supportate

| Piattaforma | File system | Guida all'installazione |
|-----|-----|-----|
| Red Hat Enterprise Linux Server 7,3, 7,4, 7,5 o 7,6 | XFS o EXT4 | [Guida all'installazione](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server V12 SP2 | XFS o EXT4 | [Guida all'installazione](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS o EXT4 | [Guida all'installazione](quickstart-install-connect-ubuntu.md) | 
| Motore Docker 1.8 + in Windows, Mac o Linux | N/D | [Guida all'installazione](quickstart-install-connect-docker.md) | 

> [!TIP]
> Per ulteriori informazioni, esaminare i [requisiti](sql-server-linux-setup.md#system) di sistema [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per in Linux. Per i criteri di supporto più [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]recenti per, vedere i [criteri di supporto tecnico per Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Strumenti

La maggior parte degli strumenti client [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esistenti destinati a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] può essere eseguita facilmente in Linux. Alcuni strumenti potrebbero avere un requisito di versione specifico per funzionare correttamente con Linux. Per un elenco completo degli [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] strumenti, vedere [strumenti e utilità SQL per SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Cronologia delle versioni

La tabella seguente elenca la cronologia delle versioni [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di.

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

## <a id="cuinstall"></a>Come installare gli aggiornamenti

Se è stato configurato il repository cu (**MSSQL-Server-2017**), si otterrà la versione più recente dei [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pacchetti quando si eseguono nuove installazioni. Il repository cu è l'impostazione predefinita per tutti gli articoli di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installazione dei pacchetti per in Linux. Se è stato configurato il repository GDR (**MSSQL-Server-2017-GDR**), si otterranno solo gli aggiornamenti critici della sicurezza rilasciati da GA. Se sono necessari gli aggiornamenti GDR o CU del contenitore Docker, vedere immagini ufficiali per [Microsoft SQL Server in Linux per il motore Docker](https://hub.docker.com/r/microsoft/mssql-server). Per altre informazioni sulla configurazione del repository, vedere [configurare repository per SQL Server in Linux](sql-server-linux-change-repo.md).

Se si aggiornano i [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pacchetti esistenti, eseguire il comando di aggiornamento appropriato per ogni pacchetto per ottenere la cu più recente. Per istruzioni dettagliate sull'aggiornamento per ogni pacchetto, vedere le guide all'installazione seguenti:

- [Installa pacchetto di SQL Server](sql-server-linux-setup.md#upgrade)
- [Installare il pacchetto di ricerca full-text](sql-server-linux-setup-full-text-search.md)
- [Installare SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Abilita SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="CU15"></a>CU15 (2019 maggio)

Questa è la versione dell'aggiornamento cumulativo 15 (CU15) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3162.1. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/en-us/help/4498951](https://support.microsoft.com/en-us/help/4498951)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3162.1-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3162.1-1 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3162.1-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU14"></a>CU14 (Mar 2019)

Questa è la versione dell'aggiornamento cumulativo 14 (CU14) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3076.1. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4484710](https://support.microsoft.com/help/4484710)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3076.1-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3076.1-2 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3076.1-2 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU13"></a>CU13 (Dec 2018)

Si tratta della versione dell'aggiornamento cumulativo 13 (CU13) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3048.4. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4466404](https://support.microsoft.com/help/4466404)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3048.4-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3048.4-1 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3048.4-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a>CU12 (Oct 2018)

Si tratta della versione dell'aggiornamento cumulativo 12 (CU12) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3045.24. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4464082](https://support.microsoft.com/help/4464082)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3045.24-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3045.24-1 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3045.24-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a>CU11 (settembre 2018)

Questa è la versione dell'aggiornamento cumulativo 11 (CU11) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3038.14. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4462262](https://support.microsoft.com/help/4462262)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3038.14-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3038.14-2 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3038.14-2 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a>CU10 dalla (agosto 2018)

Si tratta della versione dell'aggiornamento cumulativo 10 (CU10 dalla) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3037.1. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4342123](https://support.microsoft.com/help/4342123)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3037.1-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3037.1-2 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3037.1-2 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a>CU9-GDR2 (agosto 2018)

Si tratta di un aggiornamento della sicurezza che include anche la versione di CU rilasciata in precedenza (CU9) per [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3035.2. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4293805](https://support.microsoft.com/help/4293805)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3035.2-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| Pacchetto SLES RPM | 14.0.3035.2-1 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3035.2-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a>GDR2 (agosto 2018)

Si tratta di un aggiornamento della sicurezza che include solo le correzioni di sicurezza GDR2 (e [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]GDR1) per.  La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.2002.14. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4293803](https://support.microsoft.com/help/4293803)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.2002.14-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.2002.14-1 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.2002.14-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a>CU9 (luglio 2018)

Si tratta della versione dell'aggiornamento cumulativo 9 (CU9) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3030.27. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4341265](https://support.microsoft.com/help/4341265)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3030.27-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3030.27-1 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3030.27-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a>CU8 (giu 2018)

Si tratta della versione dell'aggiornamento cumulativo 8 (CU8) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3029.16. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4338363](https://support.microsoft.com/help/4338363)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3029.16-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3029.16-1 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3029.16-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a>CU7 (2018 maggio)

Questa è la versione dell'aggiornamento cumulativo 7 (CU7) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3026.27. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4229789](https://support.microsoft.com/help/4229789)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3026.27-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3026.27-2 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3026.27-2 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a>CU6 (2018 aprile)

Questa è la versione dell'aggiornamento cumulativo 6 (CU6) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3025.34. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4101464](https://support.microsoft.com/help/4101464)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3025.34-3 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3025.34-3 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3025.34-3 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a>CU5 (Mar 2018)

Questa è la versione dell'aggiornamento cumulativo 5 (CU5) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3023.8. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4092643](https://support.microsoft.com/help/4092643)versione, vedere.

### <a name="known-upgrade-issue"></a>Problema di aggiornamento noto

Quando si esegue l'aggiornamento da una versione precedente a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] CU5, potrebbe non essere possibile avviare con l'errore seguente:

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

Per correggere l'errore, abilitare SQL Server Agent e riavviare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con i comandi seguenti:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3023.8-5 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3023.8-5 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3023.8-5 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a>CU4 (feb 2018)

Si tratta della versione dell'aggiornamento cumulativo 4 (CU4) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3022.28. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4056498](https://support.microsoft.com/help/4056498)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

> [!NOTE]
> A partire da CU4, SQL Server Agent non viene più installato come pacchetto separato. Viene installato con il pacchetto del motore e deve essere abilitato per l'uso di.

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3022.28-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3022.28-2 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3022.28-2 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a>GDR1 (Jan 2018)

Si tratta di un aggiornamento della sicurezza che include solo le correzioni di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]sicurezza GDR1 per. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.2000.63. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4057122](https://support.microsoft.com/help/4057122)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.2000.63-3 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.2000.63-3 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.2000.63-3 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a>CU3 (Jan 2018)

Questa è la versione dell'aggiornamento cumulativo 3 (CU3) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3015.40. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4052987](https://support.microsoft.com/help/4052987)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3015.40-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto di SQL Server Agent RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3015.40-1 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacchetto di SQL Server Agent RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3015.40-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server Agent pacchetto Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a>CU2 (nov 2017)

Questa è la versione dell'aggiornamento cumulativo 2 (CU2) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3008.27. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3008.27-1 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto di SQL Server Agent RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3008.27-1 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacchetto di SQL Server Agent RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3008.27-1 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server Agent pacchetto Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a>CU1 (Oct 2017)

Questa è la versione dell'aggiornamento cumulativo 1 (CU1) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.3006.16. Per informazioni sulle correzioni e sui miglioramenti apportati in questa [https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634)versione, vedere.

### <a name="package-details"></a>Dettagli del pacchetto

Per le installazioni di pacchetti manuali o offline, è possibile scaricare i pacchetti RPM e Debian con le informazioni riportate nella tabella seguente:

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.3006.16-3 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto di SQL Server Agent RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.3006.16-3 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacchetto di SQL Server Agent RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.3006.16-3 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server Agent pacchetto Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a>GA (Oct 2017)

Si tratta della versione di disponibilità generale (GA) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]di. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versione per questa versione è 14.0.1000.169.

### <a name="package-details"></a>Dettagli del pacchetto

I dettagli del pacchetto e i percorsi di download per i pacchetti RPM e Debian sono elencati nella tabella seguente. Si noti che non è necessario scaricare questi pacchetti direttamente se si usano i passaggi nelle guide di installazione seguenti:

- [Installa pacchetto di SQL Server](sql-server-linux-setup.md)
- [Installare il pacchetto di ricerca full-text](sql-server-linux-setup-full-text-search.md)
- [Installa pacchetto di SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [Installare SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| Pacchetto | Versione pacchetto | Download |
|-----|-----|-----|
| Pacchetto Red Hat RPM | 14.0.1000.169-2 | [Pacchetto RPM motore](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto di SQL Server Agent RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacchetto SLES RPM | 14.0.1000.169-2 | [MSSQL-pacchetto RPM del motore del server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto RPM a disponibilità elevata](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto RPM per la ricerca full-text](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacchetto di SQL Server Agent RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Pacchetto Debian Ubuntu 16,04 | 14.0.1000.169-2 | [Pacchetto Debian del motore](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Pacchetto Debian a disponibilità elevata](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Pacchetto Debian per la ricerca full-text](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server Agent pacchetto Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[Pacchetto SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a>Funzionalità non supportate & servizi

Le funzionalità e i servizi seguenti non sono disponibili in Linux al momento della versione GA. Il supporto di queste funzionalità sarà sempre più abilitato nel tempo.

| Area | Funzionalità o servizio non supportato |
|-----|-----|
| **Motore di database** | Replica transazionale |
| &nbsp; | Replica di tipo merge |
| &nbsp; | Change Data Capture (vedere SQL Server Agent) |
| &nbsp; | Estendi database |
| &nbsp; | PolyBase |
| &nbsp; | Query distribuita con connessioni di terze parti |
| &nbsp; | Server collegati a origini dati diverse da[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | Stored procedure estese di sistema (XP_CMDSHELL e così via) |
| &nbsp; | FileTable, FILESTREAM |
| &nbsp; | Assembly CLR con il set di autorizzazioni EXTERNAL_ACCESS o unsafe |
| &nbsp; | Estensione pool di buffer |
| **SQL Server Agent** |  Sottosistemi CmdExec, PowerShell, lettura coda, SSIS, SSAS, SSRS |
| &nbsp; | Avvisi |
| &nbsp; | Agente di lettura log |
| &nbsp; | Change Data Capture (CDC) |
| &nbsp; | Backup gestito |
| **Disponibilità elevata** | Mirroring del database  |
| **Sicurezza** | Extensible Key Management |
| &nbsp; | Autenticazione AD per server collegati | 
| &nbsp; | Autenticazione AD per i gruppi di disponibilità (AGs) | 
| &nbsp; | strumenti AD di terze parti (Centrify, Vintela, Powerbroker) | 
| **Services** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |
| &nbsp; | Distributed Transaction Coordinator (DTC) |

## <a name="known-issues"></a>Problemi noti

Le sezioni seguenti descrivono i problemi noti della versione GA (General Availability) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] di in Linux.

#### <a name="general"></a>Generale

- La lunghezza del nome host in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cui è installato deve essere di 15 caratteri o meno. 

    - **Risoluzione**: Modificare il nome in/etc/hostname a un massimo di 15 caratteri.

- Se si imposta manualmente l'ora [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] di sistema indietro nel tempo, si interrompe l'aggiornamento dell'ora di sistema interna all'interno [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]di.

    - **Risoluzione**: Riavviare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

- Sono supportate solo le installazioni a istanza singola.

    - **Risoluzione**: Se si vuole avere più di un'istanza in un determinato host, è consigliabile usare VM o contenitori docker. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Configuration Manager non è possibile [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] connettersi a in Linux.

- La lingua predefinita dell'account di accesso **sa** è l'inglese.

    - **Risoluzione**: Modificare la lingua dell'account di accesso **sa** con l'istruzione **ALTER LOGIN** .

#### <a name="databases"></a>Database

- Non è possibile spostare il database master con l'utilità MSSQL-conf. È possibile spostare altri database di sistema con MSSQL-conf.

- Quando si ripristina un database di cui è stato eseguito [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] il backup in Windows, è necessario utilizzare la clausola **with Move** nell'istruzione Transact-SQL.

- Le transazioni distribuite che richiedono il servizio Microsoft Distributed Transaction Coordinator non sono [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supportate nell'esecuzione in Linux. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]i [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] server collegati sono supportati a meno che non comportino il DTC. Per altre informazioni, vedere [transazioni distribuite che richiedono il servizio Microsoft Distributed Transaction Coordinator non sono supportate in SQL Server in esecuzione su Linux](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/).

- Alcuni algoritmi (pacchetti di crittografia) per Transport Layer Security (TLS) non funzionano correttamente con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux. In questo modo si verificano errori di connessione durante il [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]tentativo di connessione a, nonché problemi di stabilire connessioni tra repliche in gruppi a disponibilità elevata.

   - **Risoluzione**: Modificare lo script di configurazione **MSSQL. conf** per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux per disabilitare i pacchetti di crittografia problematici, effettuando le operazioni seguenti:

      1. Aggiungere quanto segue a/var/opt/MSSQL/MSSQL.conf.

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

- [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]i database in Windows che usano OLTP in memoria non possono essere ripristinati [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] in Linux. Per ripristinare un [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] database che utilizza OLTP in memoria, aggiornare prima i database a [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] o [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] in Windows prima di spostarli [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in in Linux tramite backup/ripristino o scollegamento/collegamento.

- L'autorizzazione dell'utente **amministrare le operazioni bulk** non è attualmente supportata in Linux.

#### <a name="networking"></a>Rete

Le funzionalità che coinvolgono le connessioni TCP in uscita dal processo sqlservr, ad esempio i server collegati o i gruppi di disponibilità, potrebbero non funzionare se vengono soddisfatte entrambe le condizioni seguenti:

1. Il server di destinazione è specificato come nome host e non come indirizzo IP.

1. L'istanza di origine dispone di IPv6 disabilitato nel kernel. Per verificare se il sistema dispone di IPv6 abilitato nel kernel, è necessario che vengano superati tutti i test seguenti:

   - `cat /proc/cmdline`stamperà il cmdline di avvio del kernel corrente. L'output non deve contenere `ipv6.disable=1`.
   - La directory/proc/sys/net/IPv6/deve esistere.
   - Un programma C che chiama `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` deve avere esito positivo, syscall deve restituire un FD! =-1 e non ha esito negativo con EAFNOSUPPORT.

L'errore esatto dipende dalla funzionalità. Per i server collegati, questo si manifesta come errore di timeout di accesso. Per i gruppi di disponibilità `ALTER AVAILABILITY GROUP JOIN` , il linguaggio DDL sul database secondario avrà esito negativo dopo 5 minuti con un errore di timeout della configurazione di download.

Per risolvere il problema, eseguire una delle operazioni seguenti:

1. Usare gli indirizzi IP anziché i nomi host per specificare la destinazione della connessione TCP.

1. Abilitare IPv6 nel kernel rimuovendo `ipv6.disable=1` dal cmdline di avvio. La modalità di esecuzione di questa operazione dipende dalla distribuzione di Linux e dal bootloader, ad esempio grub. Se si desidera che IPv6 venga disabilitato, è comunque possibile disabilitarlo `net.ipv6.conf.all.disable_ipv6 = 1` impostando `sysctl` nella configurazione (ad esempio `/etc/sysctl.conf`). Questa operazione impedirà comunque alla scheda di rete del sistema di ottenere un indirizzo IPv6, ma consente di utilizzare le funzionalità di sqlservr.

#### <a name="network-file-system-nfs"></a>NFS (Network File System)
Se si usano condivisioni remote **NFS (Network File System)** in produzione, tenere presenti i requisiti di supporto seguenti:

- Usare NFS versione **4,2 o successiva**. Le versioni precedenti di NFS non supportano le funzionalità necessarie, ad esempio fallocate e la creazione di file sparse, comuni ai file System moderni.
- Individuare solo le directory **/var/opt/MSSQL** nel montaggio NFS. Gli altri file, ad esempio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] i file binari di sistema, non sono supportati.
- Assicurarsi che i client NFS usino l'opzione ' NOLOCK ' per il montaggio della condivisione remota.

#### <a name="localization"></a>Localizzazione

- Se le impostazioni locali non sono in inglese (en_US) durante l'installazione, è necessario usare la codifica UTF-8 nella sessione/terminale bash. Se si usa la codifica ASCII, potrebbe essere visualizzato un errore simile al seguente:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Se non è possibile usare la codifica UTF-8, eseguire il programma di installazione usando la variabile di ambiente MSSQL_LCID per specificare la lingua scelta.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Quando si esegue l'installazione di MSSQL-conf e si esegue un'installazione non [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]in lingua inglese di, i caratteri estesi non corretti vengono visualizzati dopo il testo localizzato, "Configuring SQL Server...". In alternativa, per le installazioni non basate su Latin, la frase potrebbe non essere completamente presente. La frase mancante dovrebbe visualizzare la stringa localizzata seguente: "Il PID della licenza è stato elaborato correttamente. La nuova edizione è [\<nome\> edizione] ". Questa stringa viene restituita solo a scopo informativo e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] l'aggiornamento cumulativo successivo lo risolverà per tutte le lingue. Ciò non influisce sulla corretta installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in alcun modo. 

#### <a name="full-text-search"></a>Ricerca full-text

- Non tutti i filtri sono disponibili con questa versione, inclusi i filtri per i documenti di Office. Per un elenco dei filtri supportati, vedere [Install SQL Server ricerca full-text in Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- Il pacchetto **MSSQL-Server-is** non è supportato in questa versione di SUSE. È attualmente supportata in Ubuntu e in Red Hat Enterprise Linux (RHEL).

- Con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in Linux CTP 2,1 Refresh e versioni successive [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , i pacchetti possono usare le connessioni ODBC in Linux. Questa funzionalità è stata testata con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] i driver ODBC di e MySQL, ma è anche previsto che funzioni con qualsiasi driver ODBC Unicode che osservi la specifica ODBC. In fase di progettazione è possibile specificare un DSN o una stringa di connessione per la connessione ai dati ODBC. è anche possibile usare l'autenticazione di Windows. Per altre informazioni, vedere il [post di Blog che annuncia il supporto ODBC in Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Le funzionalità seguenti non sono supportate in questa versione quando si eseguono pacchetti SSIS in Linux:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]Database del catalogo
  - Esecuzione pianificata dei pacchetti da SQL Agent
  - Autenticazione di Windows
  - Componenti di terze parti
  - Change Data Capture (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]Scale Out
  - Feature Pack di Azure per SSIS
  - Supporto di Hadoop e HDFS
  - Microsoft Connector for SAP BW

Per un elenco di componenti SSIS predefiniti che non sono attualmente supportati o supportati con limitazioni, vedere [limitazioni e problemi noti per SSIS in Linux](sql-server-linux-ssis-known-issues.md#components).

Per altre informazioni su SSIS in Linux, vedere gli articoli seguenti:
-   [Post di Blog che annuncia il supporto SSIS per Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Installare SQL Server Integration Services (SSIS) in Linux](sql-server-linux-setup-ssis.md)
-   [Estrarre, trasformare e caricare i dati in Linux con SSIS](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SQL Server Management Studio (SSMS)

Le limitazioni seguenti si applicano a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] in Windows connessa a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux.

- I piani di manutenzione non sono supportati.

- Management Data Warehouse (MDW) e l'agente di raccolta [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] dati in non sono supportati. 

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]I componenti dell'interfaccia utente con l'autenticazione di Windows o le opzioni del registro eventi di Windows non funzionano con Linux. È comunque possibile usare queste funzionalità con altre opzioni, ad esempio gli account di accesso SQL. 

- Non è possibile modificare il numero di file di log da conservare.

## <a name="next-steps"></a>Passaggi successivi

Per iniziare, vedere le guide introduttive seguenti:

- [Installa in Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installa in SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Eseguire l'installazione in Ubuntu](quickstart-install-connect-ubuntu.md)
- [Esegui in Docker](quickstart-install-connect-ubuntu.md)
- [Eseguire il provisioning di una macchina virtuale SQL in Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Esecuzione e connessione - Cloud](quickstart-install-connect-clouds.md)

Per le risposte alle domande più frequenti, vedere le domande [frequenti su SQL Server in Linux](sql-server-linux-faq.md).
