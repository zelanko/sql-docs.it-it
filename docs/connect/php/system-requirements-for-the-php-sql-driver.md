---
title: Requisiti di sistema dei driver Microsoft per PHP per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b601d4fbb02b489aca228acb719cfe8bad834dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992573"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Requisiti di sistema dei driver Microsoft per PHP per SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Questo documento elenca i componenti che devono essere installati nel sistema per accedere ai dati in un SQL Server o nel database SQL di Azure [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]tramite il.

Sono ufficialmente supportate le versioni 3,1 e successive dei driver Microsoft PHP per SQL Server. Per informazioni dettagliate sui cicli di vita del supporto e sui requisiti, incluse le versioni precedenti dei driver PHP, vedere la [matrice di supporto](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md).

## <a name="php"></a>PHP

Per informazioni su come scaricare e installare i file binari PHP stabili più recenti, vedere [il sito Web PHP](https://php.net).  I driver Microsoft per PHP per SQL Server richiedono le seguenti versioni di PHP:

|PHP per SQL Server versione del driver&#8594;<br />&#8595; Versione PHP|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|:---:|---|---|---|---|---|---|---|
|7.3|7.3.0+ | | | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>| | | | |
|7.1|7.1.0+ |7.1.0+ |7.1.0+ |7.1.0+ |       |        |        |
|7.0|       |7.0.0+ |7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |       |       |5.6.4+  |        |
|5.5|       |       |       |       |       |5.5.16+ |5.5.16+ |
|5.4|       |       |       |       |       |5.4.32  |5.4.32  |

1. Le versioni 7.2.1 e successive sono supportate in Windows, mentre le versioni 7.2.0 e successive sono supportate in Linux e macOS.

-   È necessario che la directory dell'estensione PHP includa una versione del file del driver. Per informazioni sui diversi file di driver, vedere [versioni del driver](#driver-versions) .  Per scaricare i driver, vedere [Scaricare i driver Microsoft per PHP per SQL Server](../../connect/php/download-drivers-php-sql-server.md). Per informazioni sulla configurazione del driver per PHP, vedere [Caricare i driver Microsoft per PHP per SQL Server](../../connect/php/loading-the-php-sql-driver.md).

-   È necessario un server Web. Il server Web deve essere configurato per eseguire PHP. Per informazioni sull'hosting di applicazioni PHP con IIS, vedere l' [esercitazione nel sito Web di php](http://docs.php.net/manual/da/install.windows.iis7.php).

    Il [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] è stato testato tramite IIS 10 con FastCGI.  

    > [!NOTE]  
    > Microsoft fornisce il supporto solo per IIS.  

## <a name="odbc-driver"></a>Driver ODBC

È necessaria la versione corretta del Microsoft ODBC Driver for SQL Server nel computer in cui è in esecuzione PHP. In [Questa pagina](https://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017)è possibile scaricare tutte le versioni supportate del driver per le piattaforme supportate.

Se si Scarica la versione di Windows del driver in una versione di Windows a 64 bit, il programma di installazione di ODBC 64-bit installa sia i driver ODBC a 32 bit che quelli a 64 bit. Se si utilizza una versione a 32 bit di Windows, utilizzare il programma di installazione di ODBC x86. Nelle piattaforme non Windows sono disponibili solo le versioni a 64 bit del driver.

|PHP per SQL Server versione del driver&#8594;<br />&#8595; Versione driver ODBC|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC Driver 17+ |S|S|S| | | | |
|Driver ODBC 13.1|S|S|S|S|S| | |
|Driver ODBC 13  | | | | |S| | |
|Driver ODBC 11  |S|S|S|S|S|S|S|

Se si usa il driver sqlsrv, [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) restituisce informazioni sulla versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft ODBC driver for SQL Server utilizzata da. [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Se si usa il driver PDO_SQLSRV, è possibile individuarne la versione tramite [PDO::getAttribute](../../connect/php/pdo-getattribute.md).  

## <a name="sql-server"></a>SQL Server

I database SQL di Azure sono supportati. Per informazioni, vedere [Connessione al database SQL di Microsoft Azure](../../connect/php/connecting-to-microsoft-azure-sql-database.md).

|PHP per SQL Server versione del driver&#8594;<br />&#8595; Versione di SQL Server|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Database SQL di Azure        |S|S|S|S| | | |
|Istanza gestita di SQL di Azure|S|S|S|S| | | |
|Azure SQL Data Warehouse  |S|S|S|S| | | |
|SQL Server 2017           |S|S|S|S| | | |
|SQL Server 2016           |S|S|S|S|S| | |
|SQL Server 2014           |S|S|S|S|S|S|S|
|SQL Server 2012           |S|S|S|S|S|S|S|
|SQL Server 2008 R2        |S|S|S|S|S|S|S|
|SQL Server 2008           | | | | |S|S|S|

## <a name="operating-systems"></a>Sistemi operativi
I sistemi operativi supportati per ogni versione del driver sono i seguenti:

|PHP per SQL Server versione del driver&#8594;<br />&#8595; Sistema operativo|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |S  |S  |S  |S  |   |   |   |
|Windows Server 2012 R2              |S  |S  |S  |S  |S  |S  |S  |
|Windows Server 2012                 |S  |S  |S  |S  |S  |S  |S  |
|Windows Server 2008 R2 SP1          |   |   |   |   |S  |S  |S  |
|Windows Server 2008 SP2             |   |   |   |   |S  |S  |S  |
|Windows 10                          |S  |S  |S  |S  |S  |   |   |
|Windows 8.1                         |S  |S  |S  |S  |S  |S  |S  |
|Windows 8                           |   |   |   |S  |S  |S  |S  |
|Windows 7 SP1                       |   |   |   |   |S  |S  |S  |
|Windows Vista SP2                   |   |   |   |   |S  |S  |S  |
|Ubuntu 18.10 (a 64 bit)               |S  |   |   |   |   |   |   |
|Ubuntu 18.04 (a 64 bit)               |S  |S  |   |   |   |   |   |
|Ubuntu 17.10 (a 64 bit)               |   |S  |S  |   |   |   |   |
|Ubuntu 16.04 (a 64 bit)               |S  |S  |S  |S  |S  |   |   |
|Ubuntu 15.10 (a 64 bit)               |   |   |   |S  |   |   |   |
|Ubuntu 15.04 (a 64 bit)               |   |   |   |   |S  |   |   |
|Debian 9 (64 bit)                   |S  |S  |S  |   |   |   |   |
|Debian 8 (64 bit)                   |S  |S  |S  |S  |   |   |   |
|Red Hat Enterprise Linux 7 (64 bit) |S  |S  |S  |S  |S  |   |   |
|SUSE Enterprise Linux 15 (64 bit)   |S  |   |   |   |   |   |   |
|SUSE Enterprise Linux 12 (64 bit)   |S  |S  |S  |   |   |   |   |
|macOS Mojave (64 bit)               |S  |   |   |   |   |   |   |
|macOS High Sierra (64 bit)          |S  |S  |   |   |   |   |   |
|macOS Sierra (a 64 bit)               |S  |S  |S  |S  |   |   |   |
|macOS El Capitan (a 64 bit)           |   |S  |S  |S  |   |   |   |

## <a name="driver-versions"></a>Versioni dei driver  
In questa sezione sono elencati i file di driver inclusi in ogni versione di [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Ogni pacchetto di installazione contiene i file di driver SQLSRV e PDO_SQLSRV nelle varianti con thread e senza thread. In Windows sono disponibili anche in varianti a 32 bit e a 64 bit. Per configurare il driver per l'uso con il runtime PHP, seguire le istruzioni di installazione in [caricamento dei driver Microsoft per php per SQL Server](../../connect/php/loading-the-php-sql-driver.md).

Nelle versioni supportate di Linux e macOS i driver appropriati possono essere installati usando il sistema di pacchetti PECL di PHP, seguendo le [istruzioni di installazione di Linux e MacOS](../../connect/php/installation-tutorial-linux-mac.md). In alternativa, è possibile scaricare i file binari predefiniti per la piattaforma dalla pagina dei [driver Microsoft per php per SQL Server](https://github.com/Microsoft/msphpsql/releases) progetto GitHub. nelle tabelle seguenti sono elencati i file presenti nei pacchetti binari predefiniti.

**Microsoft Driver 5.6 per PHP per SQL Server:**  

In Windows sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|Uso con PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_71_nts. dll a 32 bit<br />php_pdo_sqlsrv_71_nts. dll a 32 bit|7.1|no |Php7. dll a 32 bit|  
|php_sqlsrv_71_ts. dll a 32 bit <br />php_pdo_sqlsrv_71_ts.dll a 32 bit |7.1|sì|php7ts. dll a 32 bit|  
|php_sqlsrv_71_nts. dll a 64 bit<br />php_pdo_sqlsrv_71_nts. dll a 64 bit|7.1|no |Php7. dll a 64 bit|  
|php_sqlsrv_71_ts. dll a 64 bit <br />php_pdo_sqlsrv_71_ts.dll a 64 bit |7.1|sì|php7ts. dll a 64 bit|   
|php_sqlsrv_72_nts. dll a 32 bit<br />php_pdo_sqlsrv_72_nts. dll a 32 bit|7.2|no |Php7. dll a 32 bit|  
|php_sqlsrv_72_ts. dll a 32 bit <br />php_pdo_sqlsrv_72_ts.dll a 32 bit |7.2|sì|php7ts. dll a 32 bit|  
|php_sqlsrv_72_nts. dll a 64 bit<br />php_pdo_sqlsrv_72_nts. dll a 64 bit|7.2|no |Php7. dll a 64 bit|  
|php_sqlsrv_72_ts. dll a 64 bit <br />php_pdo_sqlsrv_72_ts.dll a 64 bit |7.2|sì|php7ts. dll a 64 bit|  
|php_sqlsrv_73_nts. dll a 32 bit<br />php_pdo_sqlsrv_73_nts. dll a 32 bit|7.3|no |Php7. dll a 32 bit|  
|php_sqlsrv_73_ts. dll a 32 bit <br />php_pdo_sqlsrv_73_ts.dll a 32 bit |7.3|sì|php7ts. dll a 32 bit|  
|php_sqlsrv_73_nts. dll a 64 bit<br />php_pdo_sqlsrv_73_nts. dll a 64 bit|7.3|no |Php7. dll a 64 bit|  
|php_sqlsrv_73_ts. dll a 64 bit <br />php_pdo_sqlsrv_73_ts.dll a 64 bit |7.3|sì|php7ts. dll a 64 bit|  

In Linux sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sì|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|no |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sì|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|no |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|sì|

**Microsoft Driver 5.3 per PHP per SQL Server:**  

In Windows sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|Uso con PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts. dll a 32 bit <br />php_pdo_sqlsrv_7_nts. dll a 32 bit |7.0|no |Php7. dll a 32 bit|
|php_sqlsrv_7_ts. dll a 32 bit  <br />php_pdo_sqlsrv_7_ts.dll a 32 bit  |7.0|sì|php7ts. dll a 32 bit|
|php_sqlsrv_7_nts. dll a 64 bit <br />php_pdo_sqlsrv_7_nts. dll a 64 bit |7.0|no |Php7. dll a 64 bit|  
|php_sqlsrv_7_ts. dll a 64 bit  <br />php_pdo_sqlsrv_7_ts.dll a 64 bit  |7.0|sì|php7ts. dll a 64 bit|
|php_sqlsrv_71_nts. dll a 32 bit<br />php_pdo_sqlsrv_71_nts. dll a 32 bit|7.1|no |Php7. dll a 32 bit|  
|php_sqlsrv_71_ts. dll a 32 bit <br />php_pdo_sqlsrv_71_ts.dll a 32 bit |7.1|sì|php7ts. dll a 32 bit|  
|php_sqlsrv_71_nts. dll a 64 bit<br />php_pdo_sqlsrv_71_nts. dll a 64 bit|7.1|no |Php7. dll a 64 bit|  
|php_sqlsrv_71_ts. dll a 64 bit <br />php_pdo_sqlsrv_71_ts.dll a 64 bit |7.1|sì|php7ts. dll a 64 bit|   
|php_sqlsrv_72_nts. dll a 32 bit<br />php_pdo_sqlsrv_72_nts. dll a 32 bit|7.2|no |Php7. dll a 32 bit|  
|php_sqlsrv_72_ts. dll a 32 bit <br />php_pdo_sqlsrv_72_ts.dll a 32 bit |7.2|sì|php7ts. dll a 32 bit|  
|php_sqlsrv_72_nts. dll a 64 bit<br />php_pdo_sqlsrv_72_nts. dll a 64 bit|7.2|no |Php7. dll a 64 bit|  
|php_sqlsrv_72_ts. dll a 64 bit <br />php_pdo_sqlsrv_72_ts.dll a 64 bit |7.2|sì|php7ts. dll a 64 bit|  

In Linux sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sì|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sì|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|no |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sì|

**Microsoft Driver 5.2 per PHP per SQL Server**  

In Windows sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|Uso con PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts. dll a 32 bit <br />php_pdo_sqlsrv_7_nts. dll a 32 bit |7.0|no |Php7. dll a 32 bit|
|php_sqlsrv_7_ts. dll a 32 bit  <br />php_pdo_sqlsrv_7_ts.dll a 32 bit  |7.0|sì|php7ts. dll a 32 bit|
|php_sqlsrv_7_nts. dll a 64 bit <br />php_pdo_sqlsrv_7_nts. dll a 64 bit |7.0|no |Php7. dll a 64 bit|  
|php_sqlsrv_7_ts. dll a 64 bit  <br />php_pdo_sqlsrv_7_ts.dll a 64 bit  |7.0|sì|php7ts. dll a 64 bit|
|php_sqlsrv_71_nts. dll a 32 bit<br />php_pdo_sqlsrv_71_nts. dll a 32 bit|7.1|no |Php7. dll a 32 bit|  
|php_sqlsrv_71_ts. dll a 32 bit <br />php_pdo_sqlsrv_71_ts.dll a 32 bit |7.1|sì|php7ts. dll a 32 bit|  
|php_sqlsrv_71_nts. dll a 64 bit<br />php_pdo_sqlsrv_71_nts. dll a 64 bit|7.1|no |Php7. dll a 64 bit|  
|php_sqlsrv_71_ts. dll a 64 bit <br />php_pdo_sqlsrv_71_ts.dll a 64 bit |7.1|sì|php7ts. dll a 64 bit|   
|php_sqlsrv_72_nts. dll a 32 bit<br />php_pdo_sqlsrv_72_nts. dll a 32 bit|7.2|no |Php7. dll a 32 bit|  
|php_sqlsrv_72_ts. dll a 32 bit <br />php_pdo_sqlsrv_72_ts.dll a 32 bit |7.2|sì|php7ts. dll a 32 bit|  
|php_sqlsrv_72_nts. dll a 64 bit<br />php_pdo_sqlsrv_72_nts. dll a 64 bit|7.2|no |Php7. dll a 64 bit|  
|php_sqlsrv_72_ts. dll a 64 bit <br />php_pdo_sqlsrv_72_ts.dll a 64 bit |7.2|sì|php7ts. dll a 64 bit|  

In Linux sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sì|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sì|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|no |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sì|

**Microsoft Driver 4.3 per PHP per SQL Server:**  

In Windows sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|Uso con PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts. dll a 32 bit <br />php_pdo_sqlsrv_7_nts. dll a 32 bit |7.0|no |Php7. dll a 32 bit|
|php_sqlsrv_7_ts. dll a 32 bit  <br />php_pdo_sqlsrv_7_ts.dll a 32 bit  |7.0|sì|php7ts. dll a 32 bit|
|php_sqlsrv_7_nts. dll a 64 bit <br />php_pdo_sqlsrv_7_nts. dll a 64 bit |7.0|no |Php7. dll a 64 bit|  
|php_sqlsrv_7_ts. dll a 64 bit  <br />php_pdo_sqlsrv_7_ts.dll a 64 bit  |7.0|sì|php7ts. dll a 64 bit|
|php_sqlsrv_71_nts. dll a 32 bit<br />php_pdo_sqlsrv_71_nts. dll a 32 bit|7.1|no |Php7. dll a 32 bit|  
|php_sqlsrv_71_ts. dll a 32 bit <br />php_pdo_sqlsrv_71_ts.dll a 32 bit |7.1|sì|php7ts. dll a 32 bit|  
|php_sqlsrv_71_nts. dll a 64 bit<br />php_pdo_sqlsrv_71_nts. dll a 64 bit|7.1|no |Php7. dll a 64 bit|  
|php_sqlsrv_71_ts. dll a 64 bit <br />php_pdo_sqlsrv_71_ts.dll a 64 bit |7.1|sì|php7ts. dll a 64 bit|   

In Linux sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sì|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|no |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sì|  

**Microsoft Driver 4.0 per PHP per SQL Server:**  

In Windows sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|Uso con PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|no|Php7. dll a 32 bit|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|sì|php7ts. dll a 32 bit|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|no|Php7. dll a 64 bit|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|sì|php7ts. dll a 64 bit|   

In Linux sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|no |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sì|

**Microsoft Driver 3.2 per PHP per SQL Server:**  

In Windows sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|Uso con PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|no|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sì|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|no|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sì|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|no|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|sì|php5ts.dll|  

**Microsoft Driver 3.1 per PHP per SQL Server:**  

In Windows sono incluse le seguenti versioni del driver:

|File del driver|Versione PHP|Thread-safe?|Uso con PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|no|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sì|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|no|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sì|php5ts.dll|  

## <a name="see-also"></a>Vedere anche  
[Introduzione ai driver Microsoft per PHP per SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Guida alla programmazione per i driver Microsoft per PHP per SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Riferimento all'API del driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
