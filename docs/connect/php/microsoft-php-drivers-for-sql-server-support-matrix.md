---
title: Matrice di supporto di driver Microsoft per PHP per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: ''
ms.openlocfilehash: ec5a151d79d9a66bfd65342336ad7aa3afcf567d
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744401"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Driver Microsoft PHP per SQL Server Support Matrix
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  Questa pagina contiene i criteri relativi al ciclo di vita e alla matrice del supporto di Microsoft PHP Driver per SQL Server.

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Matrice di ciclo di vita del supporto di Microsoft PHP driver e i criteri
 I criteri relativi al ciclo di vita del supporto Microsoft (MSL) forniscono informazioni trasparenti e prevedibili riguardanti il ciclo di vita del supporto dei prodotti Microsoft. Le versioni dei driver PHP 3.x, 4.x e 5.x offrono fino a cinque anni di supporto Mainstream dalla data di rilascio del driver. Il supporto "Mainstream" viene definito nel [sito Web del ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle).

 Le opzioni di supporto esteso e personalizzato non sono disponibili per Microsoft PHP Driver.

 I seguenti Microsoft PHP Driver sono supportati fino alla data di fine del supporto indicata.

|Nome del driver|Versione del pacchetto driver|Fine del supporto "Mainstream"|
|-|:-:|-|
|Driver Microsoft PHP 5.6 per SQL Server|5.6|21 febbraio 2024|
|5.3 i driver Microsoft PHP per SQL Server|5.3|20 luglio 2023|
|Driver Microsoft PHP 5.2 per SQL Server|5.2|9 febbraio 2023|
|4.3 i driver Microsoft PHP per SQL Server|4.3|6 luglio 2022|
|Microsoft PHP driver 4.0 per SQL Server|4.0|11 luglio 2021|
|3.2 i driver Microsoft PHP per SQL Server|3.2|Del 9 marzo 2020|
|3.1 i driver Microsoft PHP per SQL Server|3.1|12 dicembre 2019|

 I Microsoft PHP Driver non sono più supportati.

|Nome del driver|Versione del pacchetto driver|Fine del supporto "Mainstream"|
|-|:-:|-|
|Microsoft PHP driver 3.0 per SQL Server|3.0|6 marzo 2017|
|Microsoft PHP driver 2.0 per SQL Server|2.0|10 agosto 2015|
|Microsoft PHP driver 1.0 per SQL Server|1,0|28 aprile 2014|

## <a name="sql-server-version-certified-compatibility"></a>Certificata compatibilità di versione di SQL Server
 La matrice seguente elenca le versioni di SQL Server che sono state testate e certificate come compatibili con la versione corrispondente di driver. Microsoft si impegna a garantire la compatibilità con le versioni precedenti del driver, ma solo il versione più recente driver supportato è testati e certificati con le nuove versioni di SQL Server come SQL Server viene rilasciato.

|PHP per la versione del driver SQL Server&#8594;<br />&#8595; Versione di SQL Server|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Istanza gestita di SQL di Azure<br/> (Anteprima privata estesa)|S|S|S|S| | | | | |
|Azure SQL Data Warehouse|S|S|S|S| | | | | |
|SQL Server 2017         |S|S|S|S| | | | | |
|SQL Server 2016         |S|S|S|S|S| | | | |
|SQL Server 2014         |S|S|S|S|S|S|S| | |
|SQL Server 2012         |S|S|S|S|S|S|S|S| |
|SQL Server 2008 R2      |S|S|S|S|S|S|S|S|S|
|SQL Server 2008         | | | | |S|S|S|S|S|

## <a name="php-version-support"></a>Supporto versione PHP
 Con la versione dei driver Microsoft PHP elencata sono supportate le seguenti versioni di PHP:

|PHP per la versione del driver SQL Server&#8594;<br />&#8595; Versione PHP|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|:---:|---|---|---|---|---|---|---|---|---|
|7.3|7.3.0+          |                |                |       |       | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|       |       | | | | |
|7.1|7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |       |        |        |        |        |
|7.0|                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|                |                |                |       |       |5.6.4+  |        |        |        |
|5.5|                |                |                |       |       |5.5.16+ |5.5.16+ |        |        |
|5.4|                |                |                |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|                |                |                |       |       |        |        |5.3.0   |5.3.0   |
|5.2|                |                |                |       |       |        |        |        |5.2.4<br />5.2.13|

1. Le versioni 7.2.1 e versioni successive sono supportati in Windows, mentre le versioni 7.2.0 e versioni successive sono supportati in Linux e macOS.

## <a name="supported-operating-systems"></a>Sistemi operativi supportati
 Con la versione dei driver Microsoft PHP elencata sono supportate le versioni di sistemi operativi Windows seguenti:

|PHP per la versione del driver SQL Server&#8594;<br />&#8595; Sistema operativo|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |S  |S  |S  |S  |   |   |   |   |   |
|Windows Server 2012 R2              |S  |S  |S  |S  |S  |S  |S  |   |   |
|Windows Server 2012                 |S  |S  |S  |S  |S  |S  |S  |   |   |
|Windows Server 2008 R2 SP1          |   |   |   |   |S  |S  |S  |S  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |   |   |S  |
|Windows Server 2008 SP2             |   |   |   |   |S  |S  |S  |S  |   |
|Windows Server 2008                 |   |   |   |   |   |   |   |   |S  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |   |   |S  |
|Windows 10                          |S  |S  |S  |S  |S  |   |   |   |   |
|Windows 8.1                         |S  |S  |S  |S  |S  |S  |S  |   |   |
|Windows 8                           |   |   |   |S  |S  |S  |S  |   |   |
|Windows 7 SP1                       |   |   |   |   |S  |S  |S  |S  |   |
|Windows Vista SP2                   |   |   |   |   |S  |S  |S  |S  |S  |
|Windows XP SP3                      |   |   |   |   |   |   |   |   |S  |

 Con la versione dei driver Microsoft PHP elencata sono supportate Linux e Mac (solo 64 bit) le versioni del sistema operativo seguenti:

|PHP per la versione del driver SQL Server&#8594;<br />&#8595; Sistema operativo|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 18.10 (64 bit)               |S  |   |   |   |   |   |   |   |   |
|Ubuntu 18.04 (a 64 bit)               |S  |S  |   |   |   |   |   |   |   |
|Ubuntu 17.10 (a 64 bit)               |   |S  |S  |   |   |   |   |   |   |
|Ubuntu 16.04 (a 64 bit)               |S  |S  |S  |S  |S  |   |   |   |   |
|Ubuntu 15.10 (a 64 bit)               |   |   |   |S  |   |   |   |   |   |
|Ubuntu 15.04 (a 64 bit)               |   |   |   |   |S  |   |   |   |   |
|Debian 9 (64 bit)                   |S  |S  |S  |   |   |   |   |   |   |
|Debian 8 (64 bit)                   |S  |S  |S  |S  |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 bit) |S  |S  |S  |S  |S  |   |   |   |   |
|SUSE Enterprise Linux 15 (64 bit)   |S  |   |   |   |   |   |   |   |   |
|SUSE Enterprise Linux, 12 (64 bit)   |S  |S  |S  |   |   |   |   |   |   |
|macOS Mojave (64 bit)               |S  |   |   |   |   |   |   |   |   |
|macOS High Sierra (64 bit)          |S  |S  |   |   |   |   |   |   |   |
|macOS Sierra (a 64 bit)               |S  |S  |S  |S  |   |   |   |   |   |
|macOS El Capitan (a 64 bit)           |   |S  |S  |S  |   |   |   |   |   |

## <a name="see-also"></a>Vedere anche  
[Note sulla versione](../../connect/php/release-notes-for-the-php-sql-driver.md)

[Risorse di supporto](../../connect/php/support-resources-for-the-php-sql-driver.md)

[System Requirements](../../connect/php/system-requirements-for-the-php-sql-driver.md)
