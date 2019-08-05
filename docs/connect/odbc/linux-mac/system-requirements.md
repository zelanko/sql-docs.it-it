---
title: Requisiti di sistema (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b7e2dde267cf2c5f12140d883114565390d2e5d6
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702717"
---
# <a name="system-requirements"></a>Requisiti di sistema
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo argomento elenca i requisiti per l'uso di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS.


## <a name="microsoft-odbc-driver-13-131-and-17-for-sql-server"></a>Microsoft ODBC Driver for SQL Server versioni 13, 13.1 e 17

I driver per Linux e macOS sono disponibili solo per le versioni a 64 bit dei seguenti sistemi operativi:

|Sistema operativo|Versione del driver supportata|
|------------------------------------|--------------------------------|
|Apple OS X 10.11 (El Capitan)|13, 13.1, 17|
|Apple macOS 10.12 (Sierra)|13, 13.1, 17|
|Apple macOS 10.13 (High Sierra)|17| 
|Apple macOS 10.14 (Mojave)|17| 
|Debian Linux 8|13, 13.1, 17|
|Debian Linux 9|17|
|Debian Linux 10|17.4|
|RedHat Enterprise Linux 6|13, 13.1, 17|
|RedHat Enterprise Linux 7|13, 13.1, 17|
|RedHat Enterprise Linux 8|17.4|
|SuSE Linux Enterprise Server 11|13, 13.1, 17 <br /><br /> **NOTA:** ODBC Driver 17 supporta solo SuSE Linux Enterprise Server 11 SP4|
|SuSE Linux Enterprise Server 12|13, 13.1, 17|
|SuSE Linux Enterprise Server 15|17|
|Ubuntu Linux 14.04|13, 13.1, 17|
|Ubuntu Linux 15.10|13, 13.1|
|Ubuntu Linux 16.04|13, 13.1, 17|
|Ubuntu Linux 16.10|13, 13.1|
|Ubuntu Linux 17.04|17| 
|Ubuntu Linux 17.10|17|
|Ubuntu Linux 18.04|17| 
|Ubuntu Linux 18.10|17| 
|Ubuntu Linux 19.04|17.3| 

I pacchetti di installazione di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13, 13.1 e 17 per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS risolvono automaticamente le dipendenze del driver se installati tramite il sistema di gestione pacchetti della distribuzione, come descritto in [Installazione del driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 per SQL Server  
  
-   Gestione driver UnixODBC 2.3.0 a 64 bit per SQLLEN/SQLULEN a 64 bit. Le versioni successive di Gestione driver UnixODBC a 64 bit non sono supportate con il driver ODBC in Linux. Per ulteriori informazioni, vedere [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) .  
  
-   Il driver ODBC per **Red Hat Enterprise Linux 5 (64 bit)** richiede i pacchetti seguenti e può essere scaricato da qui: [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `e2fsprogs-libs`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   Il driver ODBC per **Red Hat Enterprise Linux 6 (64 bit)** richiede i pacchetti seguenti e può essere scaricato da qui: [Microsoft ODBC Driver 11 for SQL Server - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `libuuid`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   Il driver ODBC per **SUSE Linux Enterprise 11 Service Pack 2 (64 bit)** richiede i pacchetti seguenti e può essere scaricato da qui: [Microsoft ODBC Driver 11 Preview for SQL Server - SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)  
    -   `glibc`  
    -   `libstdc++46`  
    -   `libgcc46`  
    -   `libuuid1`  
    -   `krb5`  
    -   `libopenssl0_9_8`  
  
## <a name="see-also"></a>Vedere anche
[Installazione di Gestione driver](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Problemi noti in questa versione del driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[Note sulla versione](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
