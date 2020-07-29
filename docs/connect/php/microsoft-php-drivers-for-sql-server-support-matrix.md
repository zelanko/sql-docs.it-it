---
title: Matrice di supporto dei driver Microsoft per PHP
description: Questa pagina contiene i criteri relativi al ciclo di vita e alla matrice del supporto di Microsoft PHP Driver per SQL Server.
ms.custom: ''
ms.date: 04/15/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 635c6ecbe6404b7e5466ecf5929dd2330183e7a0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85793154"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Driver PHP Microsoft per la matrice di supporto SQL Server

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Questa pagina contiene i criteri relativi al ciclo di vita e alla matrice del supporto di Microsoft PHP Driver per SQL Server.

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Criteri e matrice del ciclo di vita del supporto dei driver PHP Microsoft

I criteri relativi al ciclo di vita del supporto Microsoft (MSL) forniscono informazioni trasparenti e prevedibili riguardanti il ciclo di vita del supporto dei prodotti Microsoft. Le versioni dei driver PHP 3.x, 4.x e 5.x offrono fino a cinque anni di supporto Mainstream dalla data di rilascio del driver. Il supporto "Mainstream" viene definito nel [sito Web del ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle).

Le opzioni di supporto esteso e personalizzato non sono disponibili per Microsoft PHP Driver.

I seguenti Microsoft PHP Driver sono supportati fino alla data di fine del supporto indicata.

|Nome del driver|Versione del pacchetto driver|Fine del supporto Mainstream|
|-|:-:|-|
|Driver PHP Microsoft 5.8 per SQL Server|5.8|31 gennaio 2025|
|Driver Microsoft PHP 5.6 per SQL Server|5.6|21 febbraio 2024|
|Driver Microsoft PHP 5.3 per SQL Server|5.3|20 luglio 2023|
|Driver Microsoft PHP 5.2 per SQL Server|5,2|9 febbraio 2023|
|Driver Microsoft PHP 4.3 per SQL Server|4.3|6 luglio 2022|
|Driver Microsoft PHP 4.0 per SQL Server|4.0|11 luglio 2021|
|Driver Microsoft PHP 3.2 per SQL Server|3.2|9 marzo 2020|
| &nbsp; | &nbsp; | &nbsp; |

I Microsoft PHP Driver non sono più supportati.

|Nome del driver|Versione del pacchetto driver|Fine del supporto Mainstream|
|-|:-:|-|
|Driver Microsoft PHP 3.1 per SQL Server|3.1|12 dicembre 2019|
|Driver Microsoft PHP 3.0 per SQL Server|3.0|6 marzo 2017|
|Driver Microsoft PHP 2.0 per SQL Server|2.0|10 agosto 2015|
|Driver Microsoft PHP 1.0 per SQL Server|1.0|28 aprile 2014|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="sql-server-version-certified-compatibility"></a>Compatibilità certificata delle versioni di SQL Server
 La matrice seguente elenca le versioni di SQL Server testate e certificate come compatibili con la versione del driver corrispondente. Microsoft si impegna a mantenere la compatibilità con le versioni precedenti del driver, ma solo il driver supportato più recente viene testato e certificato con le nuove versioni di SQL Server quando viene rilasciato SQL Server.

|PHP per la versione del driver SQL Server &#8594;<br />&#8595; Versione di SQL Server|5.8|5.6|5.3|5,2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Istanza gestita di SQL di Azure|S|S|S|S|S| | |
|Azure SQL Data Warehouse|S|S|S|S|S| | |
|SQL Server 2019         |S| | | | | | |
|SQL Server 2017         |S|S|S|S|S| | |
|SQL Server 2016         |S|S|S|S|S|S| |
|SQL Server 2014         |S|S|S|S|S|S|S|
|SQL Server 2012         |S|S|S|S|S|S|S|
|SQL Server 2008 R2      | |S|S|S|S|S|S|
|SQL Server 2008         | | | | | |S|S|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="php-version-support"></a>Supporto versione PHP

Le versioni seguenti di PHP sono supportate con la versione indicata dei driver PHP Microsoft:

|PHP per la versione del driver SQL Server &#8594;<br />&#8595; Versione PHP|5.8|5.6|5.3|5,2|4.3|4.0|3.2|
|:---:|---|---|---|---|---|---|---|
|7.4|7.4.0+          |                |                |                |       |        |        |
|7.3|7.3.0+          |7.3.0+          |                |                |       |        |        |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|       |        |        |
|7.1|                |7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |        |        |
|7.0|                |                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+  |        |
|5.6|                |                |                |                |       |        |5.6.4+  |
|5.5|                |                |                |                |       |        |5.5.16+ |
|5.4|                |                |                |                |       |        |5.4.32  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

1. Le versioni 7.2.1 e successive sono supportate in Windows, mentre le versioni 7.2.0 e successive sono supportate in Linux e macOS.

## <a name="supported-operating-systems"></a>Sistemi operativi supportati

Le versioni seguenti del sistema operativo Windows sono supportate con la versione indicata dei driver PHP Microsoft:

|PHP per la versione del driver SQL Server &#8594;<br />&#8595; Sistema operativo|5.8|5.6|5.3|5,2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2019                 |S  |S  |   |   |   |   |   |
|Windows Server 2016                 |S  |S  |S  |S  |S  |   |   |
|Windows Server 2012 R2              |S  |S  |S  |S  |S  |S  |S  |
|Windows Server 2012                 |S  |S  |S  |S  |S  |S  |S  |
|Windows Server 2008 R2 SP1          |   |   |   |   |   |S  |S  |
|Windows Server 2008 R2              |   |   |   |   |   |   |   |
|Windows Server 2008 SP2             |   |   |   |   |   |S  |S  |
|Windows 10                          |S  |S  |S  |S  |S  |S  |   |
|Windows 8.1                         |S  |S  |S  |S  |S  |S  |S  |
|Windows 8                           |   |   |   |   |S  |S  |S  |
|Windows 7 SP1                       |   |   |   |   |   |S  |S  |
|Windows Vista SP2                   |   |   |   |   |   |S  |S  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

Le versioni seguenti dei sistemi operativi Linux e macOS (solo 64 bit) sono supportate con la versione indicata dei driver PHP Microsoft:

|PHP per la versione del driver SQL Server &#8594;<br />&#8595; Sistema operativo|5.8|5.6|5.3|5,2|4.3|4.0|3.2|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 19.10 (a 64 bit)               |S  |   |   |   |   |   |   |
|Ubuntu 18.10 (a 64 bit)               |   |S  |   |   |   |   |   |
|Ubuntu 18.04 (a 64 bit)               |S  |S  |S  |   |   |   |   |
|Ubuntu 17.10 (a 64 bit)               |   |   |S  |S  |   |   |   |
|Ubuntu 16.04 (a 64 bit)               |S  |S  |S  |S  |S  |S  |   |
|Ubuntu 15.10 (a 64 bit)               |   |   |   |   |S  |   |   |
|Ubuntu 15.04 (a 64 bit)               |   |   |   |   |   |S  |   |
|Debian 10 (a 64 bit)                  |S  |   |   |   |   |   |   |
|Debian 9 (a 64 bit)                   |S  |S  |S  |S  |   |   |   |
|Debian 8 (a 64 bit)                   |S  |S  |S  |S  |S  |   |   |
|Red Hat Enterprise Linux 8 (64 bit) |S  |   |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 bit) |S  |S  |S  |S  |S  |S  |   |
|Suse Enterprise Linux 15 (64 bit)   |S  |S  |   |   |   |   |   |
|Suse Enterprise Linux 12 (64 bit)   |S  |S  |S  |S  |   |   |   |
|Alpine Linux 3.11 (64 bit)<sup>1</sup>|S  |   |   |   |   |   |   |
|macOS Catalina (64 bit)             |S  |   |   |   |   |   |   |
|macOS Mojave (64 bit)               |S  |S  |   |   |   |   |   |
|macOS High Sierra (64 bit)          |S  |S  |S  |   |   |   |   |
|macOS Sierra (a 64 bit)               |   |S  |S  |S  |S  |   |   |
|macOS El Capitan (a 64 bit)           |   |   |S  |S  |S  |   |   |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> Il supporto di Alpine Linux è sperimentale per la versione 5.8.0. La versione 5.8.1 introduce il supporto per la produzione.

## <a name="see-also"></a>Vedere anche

[Note sulla versione](release-notes-php-sql-driver.md)

[Risorse di supporto](support-resources-for-the-php-sql-driver.md)

[System Requirements](system-requirements-for-the-php-sql-driver.md)
