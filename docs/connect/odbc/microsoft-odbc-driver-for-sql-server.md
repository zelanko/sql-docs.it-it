---
title: Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/04/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9f2ae91b-06af-4c9a-9d24-062df7bc4662
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a6c86f3097efdc30089820432fedcb0ab530e04
ms.sourcegitcommit: b3d84abfa4e2922951430772c9f86dce450e4ed1
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/22/2019
ms.locfileid: "56662615"
---
# <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

ODBC è l'API di accesso ai dati nativa principale per le applicazioni scritte in C e C++ per SQL Server. È un driver ODBC per la maggior parte delle origini dati. Altri linguaggi che è possono usare ODBC includono COBOL, Perl, PHP e Python. ODBC è ampiamente usato in scenari di integrazione dati.

Il driver ODBC include strumenti come [**sqlcmd**](../../tools/sqlcmd-utility.md) e [**bcp**](../../tools/bcp-utility.md). L'utilità **sqlcmd** consente di eseguire istruzioni Transact-SQL, procedure di sistema e script SQL. L'utilità **bcp** esegue operazioni di copia bulk di dati tra un'istanza di Microsoft SQL Server e un file di dati in un formato specificato dall'utente. L'utilità **bcp** può essere usata per importare un numero elevato di nuove righe in tabelle SQL Server oppure per esportare dati da tabelle in file di dati.  

## <a name="code-example-in-c"></a>Esempio di codice in C++

L'esempio C++ seguente viene illustrato come usare le API ODBC per connettersi e accedere a un database:

- [Esempio di codice C++, tramite ODBC](../../odbc/reference/sample-odbc-program.md)

## <a name="download"></a>Scarica

- ![Download-FRECCIAGIÙ cerchiato](../../ssdt/media/download.png)[per scaricare il driver ODBC](download-odbc-driver-for-sql-server.md)

## <a name="documentation"></a>Documentazione

### <a name="features"></a>Funzionalità

- [Provider di archivi chiavi personalizzati](../../connect/odbc/custom-keystore-providers.md)
- [Parole chiave e attributi per stringhe di connessione e DSN](dsn-connection-string-attribute.md)
- [SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md) (le funzionalità disponibili sono applicabili anche, senza OLEDB, per il Driver ODBC per SQL Server)
- [Uso di Always Encrypted](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [Uso di Azure Active Directory](../../connect/odbc/using-azure-active-directory.md)
- [Uso della stringa di connessione TransparentNetworkIPResolution](../../connect/odbc/using-transparent-network-ip-resolution.md)
- [Uso delle transazioni XA](../../connect/odbc/use-xa-with-dtc.md)

### <a name="linux-and-macos"></a>Linux e macOS

- [Installazione del Driver](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Connessione a SQL Server](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)
- [Connessione a **bcp**](../../connect/odbc/linux-mac/connecting-with-bcp.md)
- [Connessione a **sqlcmd**](../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)
- [Traccia di accesso ai dati](../../connect/odbc/linux-mac/data-access-tracing-with-the-odbc-driver-on-linux.md)
- [Domande frequenti](../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)
- [Installazione di Gestione driver](../../connect/odbc/linux-mac/installing-the-driver-manager.md)
- [Problemi noti](../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)
- [Linee guida per la programmazione](../../connect/odbc/linux-mac/programming-guidelines.md)
- [Note sulla versione](../../connect/odbc/linux-mac/release-notes.md)
- [Supporto per disponibilità elevata e ripristino di emergenza](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
- [Uso dell'autenticazione integrata (Kerberos)](../../connect/odbc/linux-mac/using-integrated-authentication.md)

### <a name="windows"></a>Windows

- [Esempio di esecuzione asincrona (metodo di notifica)](../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)
- [Resilienza di connessione nel driver ODBC di Windows](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
- [Pool di connessioni compatibile con il driver](../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)
- [Le funzionalità e modifiche del comportamento](../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)
- [Note sulla versione](../../connect/odbc/windows/release-notes.md)
- [Requisiti di sistema, installazione e file del driver](../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)



## <a name="community"></a>Community  
- [Blog del team di Microsoft ODBC Driver for SQL Server](https://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [Forum di accesso ai dati di SQL Server](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
