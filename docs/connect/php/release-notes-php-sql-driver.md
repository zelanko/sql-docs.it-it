---
title: Note sulla versione dei driver Microsoft per PHP per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-dapugl, kenvh
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23ac53a8515f55dfc0cad282fd14294e5f285af9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935911"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Note sulla versione dei driver Microsoft per PHP per SQL Server

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In questa pagina vengono illustrati gli [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]elementi aggiunti in ogni versione di.  

<!--
Hello, We are standardizing the format of content inside our Release Notes (or What's New) articles.
Instead of bullets (or paragraphs), we have shifted to the 2-column format you see for H2 **What's New in Version 5.6**.
It is not necessary to reformat all the older H2 sections in this Release Notes file, but.....

Going forward, please be sure to use the 2-column format.

Also, all Release Notes .md file names now must begin with 'release-notes-*.md'.  And no filler words.
The 5.6 edition of this file is being renamed.....
FROM:  'release-notes-for-the-php-sql-driver.md'
TO  :  'release-notes-php-sql-driver.md'

For any questions, ask GeneMi or CraigG.
Thanks a lot.  2019-03-28  (DevO= 1467988)
-->

## <a name="whats-new-in-version-56"></a>Novità della versione 5.6

| Nuovo elemento | Dettagli |
| :------- | :------ |
| Supporto per PHP 7.3. | &nbsp; |
| Il supporto per PHP 7,0 è stato eliminato. | &nbsp; |
| Supporto per Microsoft ODBC driver 17,3 su tutte le piattaforme. | &nbsp; |
| Supporto per macOS Mojave. | Richiede il driver ODBC 17,3 o versione successiva. |
| Supporto per Ubuntu 18,10 e SUSE Linux 15. | Entrambi richiedono il driver ODBC 17,3 o versione successiva. |
| È stato eliminato il supporto per Linux Ubuntu 17,10 e macOS El Capitan. | &nbsp; |
| Supporto per il token di accesso Azure AD. | In Linux e macOS è necessario il driver ODBC 17,2 + e unixODBC 2.3.6 +. |
| Supporto per l'autenticazione con Azure AD usando l'identità gestita per le risorse di Azure. | Richiede il driver ODBC 17.3 +. |
| Nuove funzionalità di recupero | &bull;&nbsp; Nuovo flag DOP:: SQLSRV_ATTR_FETCHES_DATETIME_TYPE per PDO_SQLSRV per restituire DateTime come oggetti.<br/><br/>&bull;&nbsp; Aggiungere l'opzione ReturnDatesAsStrings al livello di istruzione per sqlsrv.<br/><br/>&bull;&nbsp; Nuove opzioni a livello di connessione e di istruzione per entrambi i driver per la formattazione dei valori decimali nei risultati recuperati. |
| Supporto per la compilazione statica di driver se gli utenti scelgono di eseguire la compilazione dall'origine. | &nbsp; |
| Miglioramento delle prestazioni tramite la memorizzazione dei metadati nella cache durante le operazioni di recupero e accelerazione delle conversioni di stringhe Unicode. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="whats-new-in-version-53"></a>Novità della versione 5.3

- Supporto per Microsoft ODBC driver 17,2 su tutte le piattaforme
- Supporto per macOS High Sierra (richiede ODBC driver 17 e versioni successive)
- Supporto per Azure Key Vault per Always Encrypted per le funzionalità CRUD di base, in modo che Always Encrypted funzionalità sia disponibile per tutte le piattaforme Windows, Linux o macOS supportate [usando always Encrypted con i driver php per SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
- Supporto di Ubuntu 18,04 LTS (richiede il driver ODBC 17,2)
- Supporto per la resilienza delle connessioni anche in Linux o macOS (richiede il driver ODBC 17,2)

## <a name="whats-new-in-version-52"></a>Novità della versione 5.2

- Supporto per 7.2.1 PHP e su Windows e 7.2.0 e su altre piattaforme
- Supporto per Microsoft ODBC driver 17
  - La versione 17 è ora l'impostazione predefinita in tutte le piattaforme
- Supporto per Ubuntu 17,10, Debian 9 e SUSE Enterprise Linux 12
- Eliminazione del supporto per Ubuntu 15,10
- Supporto per Always Encrypted con funzionalità CRUD in Windows. Per altre informazioni, vedere [Uso di Always Encrypted con i driver PHP per SQL Server](../../connect/php/using-always-encrypted-php-drivers.md).
  - Supporto per l'archivio certificati di Windows
  - Always Encrypted è supportato solo con Microsoft ODBC driver 17 e versioni successive
- Supporto per le impostazioni locali non UTF8 in Linux e macOS
  - Le impostazioni locali non UTF8 in Linux e macOS sono supportate solo con Microsoft ODBC driver 17 e versioni successive
- Supporto per Azure SQL Data Warehouse
- Supporto per l'istanza gestita di database SQL di Azure (anteprima privata estesa)

## <a name="whats-new-in-version-43"></a>Novità della versione 4.3

- Supporto per PHP 7.1
- Supporto per macOS Sierra e macOS El Capitan
- Supporto per Ubuntu 15,10 e Debian 8
- Eliminazione del supporto per Ubuntu 15,04
- Supporto per i gruppi di disponibilità Always On tramite la risoluzione IP di rete trasparente. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md).
- Aggiunta del supporto per il tipo di dati sql_variant con limitazione.
- Supporto per la resilienza delle connessioni inattive in Windows. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md).
- Supporto del pool di connessioni per Linux e macOS. Per altre informazioni, vedere [Pool di connessioni](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).
- Supporto per l'autenticazione Azure Active Directory con ActiveDirectoryPassword e sqlpassword. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md).

## <a name="whats-new-in-version-40"></a>Novità della versione 4.0

- Supporto per PHP 7.0  
- Supporto completo a 64 bit
- Supporto per Ubuntu 15.04, Ubuntu 16.04 e RedHat 7

## <a name="whats-new-in-version-32"></a>Novità della versione 3.2

- Supporto per PHP 5.6   
- Include gli aggiornamenti più recenti per le versioni precedenti di PHP, la 5.5 e la 5.4   
- Richiede Microsoft ODBC Driver 11 per SQL Server  

## <a name="whats-new-in-version-31"></a>Novità della versione 3.1

- Supporto per PHP 5.5  
- Richiede Microsoft ODBC Driver 11 per SQL Server. Le versioni precedenti richiedono SQL Native Client.  

## <a name="whats-new-in-version-30"></a>Novità della versione 3.0  

- Supporto per PHP 5.4  PHP 5.2 non è supportato nella versione 3 di [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
- È stata aggiunta l'opzione di connessione AttachDBFileName. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md).  
- Supporto per Local DB, aggiunto in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Per ulteriori informazioni, vedere [supporto per il database locale](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).
- È stata aggiunta l'opzione di connessione AttachDBFileName. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md).  
- Supporto per le funzionalità di ripristino di emergenza a disponibilità elevata. Per altre informazioni, vedere [Supporto per disponibilità elevata e ripristino di emergenza](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).
- Supporto per i cursori sul lato client (memorizzazione nella cache di un set di risultati in memoria). Per altre informazioni, vedere [Tipi di cursore &#40;driverSQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md) e [Tipi di cursore &#40;driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- È stato aggiunto l'attributo PDO::ATTR_EMULATE_PREPARES. Per altre informazioni, vedere [PDO::prepare](../../connect/php/pdo-prepare.md).  

## <a name="whats-new-in-version-20"></a>Novità della versione 2.0

Nella versione 2.0 è stato aggiunto il supporto per il driver PDO_SQLSRV. Per altre informazioni, vedere [Guida di riferimento del driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md).  

## <a name="see-also"></a>Vedere anche

[Panoramica dei driver Microsoft per PHP per SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
