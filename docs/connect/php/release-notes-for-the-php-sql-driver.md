---
title: Note sulla versione dei driver Microsoft per PHP per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c2e7377b1072c30e5c5ef038b93a88f0c222260
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744351"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Note sulla versione dei driver Microsoft per PHP per SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Questo argomento vengono illustrate le funzionalità aggiunte in ogni versione del [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

## <a name="whats-new-in-version-56"></a>Novità della versione 5.6

- Supporto per PHP 7.3
- Supporto per Microsoft ODBC Driver 17.3 su tutte le piattaforme
- Supporto per macOS Mojave (richiede la versione 17.3 Driver ODBC o versioni successive)
- Supporto per 18.10 Ubuntu e Suse Linux 15 (entrambi richiedono di ODBC Driver 17.3 o successiva)
- Eliminato il supporto per PHP 7.0
- Eliminazione del supporto per Linux Ubuntu 17.10 e macOS El Capitan
- Supporto per il Token di accesso di Azure AD (in Linux e macOS, richiede unixODBC 2.3.6+ e Driver ODBC 17.2 +)
- Supporto per l'autenticazione con Azure AD con un'identità gestita per le risorse di Azure (richiede il Driver ODBC versione 17.3 +)
- Nuove funzionalità di recupero:
  - Nuovo contrassegno PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE per pdo_sqlsrv restituire datetime come oggetti
  - Aggiunta opzione ReturnDatesAsStrings a livello di istruzione per sqlsrv
  - Nuove opzioni a livello di connessione e istruzione per entrambi i driver per la formattazione di valori decimali nei risultati recuperati
- Supporto per la compilazione statica di driver, se gli utenti scelgono per compilarle dal codice sorgente
- Miglioramento delle prestazioni tramite la memorizzazione nella cache dei metadati in recuperi e velocizzare le conversioni di stringhe Unicode

## <a name="whats-new-in-version-53"></a>Novità della versione 5.3

- Supporto per Microsoft ODBC Driver 17.2 su tutte le piattaforme
- Supporto per macOS High Sierra (richiede ODBC Driver 17 e versioni successive)
- Per Azure Key Vault per Always Encrypted basic CRUD le funzionalità di questo tipo che è disponibile a tutte le funzionalità crittografia sempre attiva supporto per piattaforme Windows, Linux o macOS [uso di Always Encrypted con il driver PHP per SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
- Supporto di Ubuntu LTS 18.04 (richiede ODBC Driver 17.2)
- Supporto per la resilienza della connessione in Linux o macOS anche (richiede ODBC Driver 17.2)

## <a name="whats-new-in-version-52"></a>Novità della versione 5.2

- Supporto per PHP 7.2.1 e backup in Windows e 7.2.0 e su altre piattaforme
- Supporto per Microsoft ODBC Driver 17
  - Versione 17 è ora l'impostazione predefinita in tutte le piattaforme
- Supporto per Ubuntu 17.10, Debian 9 ed Enterprise Suse Linux 12
- Eliminato il supporto per Ubuntu 15.10
- Supporto per Always Encrypted con funzionalità CRUD su Windows. Per altre informazioni, vedere [uso di Always Encrypted con il driver PHP per SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
  - Supporto per Windows Store di certificato
  - Always Encrypted è supportato solo con Microsoft ODBC Driver 17 e versioni successive
- Supporto per le impostazioni locali non UTF8 in Linux e macOS
  - Le impostazioni locali non UTF8 in Linux e macOS sono supportate solo con Microsoft ODBC Driver 17 e versioni successive
- Supporto per Azure SQL Data Warehouse
- Supporto per l'istanza gestita SQL di Azure (anteprima privata estesa)


## <a name="whats-new-in-version-43"></a>Novità della versione 4.3

- Supporto per PHP 7.1
- Supporto per macOS Sierra e macOS El Capitan
- Supporto per Ubuntu 15.10 e Debian 8
- Eliminato il supporto per Ubuntu 15.04
- Supporto per i gruppi di disponibilità Always On tramite risoluzione dell'IP di rete trasparente. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md).
- Aggiunta del supporto per il tipo di dati sql_variant con limitazione.
- Supporto di resilienza delle connessioni inattivo in Windows. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md).
- Pool di connessioni di supporto per Linux e macOS. Per altre informazioni, vedere [Pool di connessioni](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).
- Supporto per l'autenticazione di Azure Active Directory con ActiveDirectoryPassword e SqlPassword. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md).

## <a name="whats-new-in-version-40"></a>Novità della versione 4.0

- Supporto per PHP 7.0  
- Supporto a 64 bit
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
- Supporto per Local DB, aggiunto in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Per altre informazioni, vedere [supporto per LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).
- È stata aggiunta l'opzione di connessione AttachDBFileName. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md).  
- Supporto per le funzionalità di ripristino di emergenza a disponibilità elevata. Per altre informazioni, vedere [supporto per la disponibilità elevata, ripristino di emergenza](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).
- Supporto per i cursori sul lato client (memorizzazione nella cache di un set di risultati in memoria). Per altre informazioni, vedere [Tipi di cursore &#40;driverSQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md) e [Tipi di cursore &#40;driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- È stato aggiunto l'attributo PDO::ATTR_EMULATE_PREPARES. Per altre informazioni, vedere [PDO::prepare](../../connect/php/pdo-prepare.md).  

## <a name="whats-new-in-version-20"></a>Novità della versione 2.0  
Nella versione 2.0 è stato aggiunto il supporto per il driver PDO_SQLSRV. Per altre informazioni, vedere [Guida di riferimento del driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md).  

## <a name="see-also"></a>Vedere anche  
[Panoramica dei driver Microsoft per PHP per SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
