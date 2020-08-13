---
title: Requisiti di sistema (ODBC Driver for SQL Server)
description: In questo articolo sono indicati i requisiti di sistema per ODBC Driver for SQL Server nei sistemi operativi Linux e macOS.
ms.custom: ''
ms.date: 03/18/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01a5dd44d111fd72d76db244c8135d3bdde00ec8
ms.sourcegitcommit: cb620c77fe6bdefb975968837706750c31048d46
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2020
ms.locfileid: "86391756"
---
# <a name="system-requirements-linux-and-macos"></a>Requisiti di sistema (Linux e macOS)

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo argomento elenca i requisiti per l'uso di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS.

## <a name="sql-version-compatibility"></a>Compatibilità tra versioni SQL

La compatibilità tra versioni SQL per i driver Linux e macOS e uguale alla [compatibilità tra versioni SQL dei driver Windows](../windows/system-requirements-installation-and-driver-files.md#sql-version-compatibility).

## <a name="operating-system-support"></a>Supporto dei sistemi operativi

Le versioni 17, 13.1 e 13 dei driver per Linux e macOS sono supportate solo sull'architettura x64 dei sistemi operativi seguenti:

|Sistemi operativi supportati     |17.5|17.4|17.3|17.2|17.1|17.0|13.1|13|
|-------------------------------|----|----|----|----|----|----|----|--|
|Apple OS X 10.11 (El Capitan)  | |S|S|S|S|S|S|S|
|Apple macOS 10.12 (Sierra)     | |S|S|S|S|S|S|S|
|Apple macOS 10.13 (High Sierra)|S|S|S|S|S|S|S|S|
|Apple macOS 10.14 (Mojave)     |S|S|S| | | | | |
|Apple macOS 10.15 (Catalina)   |S| | | | | | | |
|Alpine Linux 3.11              |S| | | | | | | |
|Debian Linux 8                 | |S|S|S|S|S|S|S|
|Debian Linux 9                 |S|S|S|S|S|S|S|S|
|Debian Linux 10                |S|S| | | | | | |
|Oracle Linux 8                 |S| | | | | | | |
|RedHat Enterprise Linux 6      |S|S|S|S|S|S|S|S|
|RedHat Enterprise Linux 7      |S|S|S|S|S|S|S|S|
|RedHat Enterprise Linux 8      |S|S| | | | | | |
|SUSE Linux Enterprise Server 11<sup>1</sup>|S|S|S|S|S|S|S|S|
|SUSE Linux Enterprise Server 12|S|S|S|S|S|S|S|S|
|SUSE Linux Enterprise Server 15|S|S|S| | | | | |
|Ubuntu Linux 14.04             | |S|S|S|S|S|S|S|
|Ubuntu Linux 16.04             |S|S|S|S|S|S|S|S|
|Ubuntu Linux 18.04             |S|S|S|S| | | | |
|Ubuntu Linux 19.10             |S| | | | | | | |

<sup>1</sup> ODBC Driver 17 supporta solo SUSE Linux Enterprise Server 11 SP4

I pacchetti di installazione di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13, 13.1 e 17 per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS risolvono automaticamente le dipendenze del driver se installati tramite il sistema di gestione pacchetti della distribuzione, come descritto in [Installare il driver ODBC (Linux)](installing-the-microsoft-odbc-driver-for-sql-server.md) e [Installare il driver ODBC (macOS)](install-microsoft-odbc-driver-sql-server-macos.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 per SQL Server  
  
* Gestione driver UnixODBC 2.3.0 a 64 bit per SQLLEN/SQLULEN a 64 bit. Le versioni successive di Gestione driver UnixODBC a 64 bit non sono supportate con il driver ODBC in Linux. Per ulteriori informazioni, vedere [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) .  
  
* Il driver ODBC per **Red Hat Enterprise Linux 5 (64 bit)** richiede i pacchetti seguenti e può essere scaricato da qui: [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `e2fsprogs-libs`  
  * `krb5-libs`  
  * `openssl`  
  
* Il driver ODBC per **Red Hat Enterprise Linux 6 (64 bit)** richiede i pacchetti seguenti e può essere scaricato da qui: [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `libuuid`  
  * `krb5-libs`  
  * `openssl`  
  
* Il driver ODBC per **SUSE Linux Enterprise 11 Service Pack 2 (64 bit)** richiede i pacchetti seguenti e può essere scaricato da qui: [Microsoft ODBC Driver 11 Preview for SQL Server - SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)  
  * `glibc`  
  * `libstdc++46`  
  * `libgcc46`  
  * `libuuid1`  
  * `krb5`  
  * `libopenssl0_9_8`  
  
## <a name="see-also"></a>Vedere anche

[Installazione di Gestione driver](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)  
[Problemi noti in questa versione del driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  
[Note sulla versione](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
