---
title: Elenco di bug corretti | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 096c11c018294cbc92b2be13801d6cd953548fff
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264014"
---
# <a name="list-of-bugs-fixed"></a>Elenco di bug corretti

Questa pagina contiene un elenco dei bug corretti in ogni versione, a partire [!INCLUDE[msCoName](../../includes/msconame_md.md)] da ODBC driver 17 for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd"></a>Correzioni di bug nel [!INCLUDE[msCoName](../../includes/msconame_md.md)] driver ODBC 17,3 per[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Perdita di memoria del gestore eventi di notifica trasmissione TCP
- Correzione del problema di ridefinizione dell'enumerazione _SQL_FILESTREAM_DESIRED_ACCESS nel file di intestazione msodbcsql. h
- Correzione della definizione del ACCESS_TOKEN mancante e della definizione correlata all'autenticazione nel file di intestazione msodbcsql. h per Linux

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd"></a>Correzioni di bug nel [!INCLUDE[msCoName](../../includes/msconame_md.md)] driver ODBC 17,2 per[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correzione di un messaggio di errore relativo all'autenticazione Azure Active Directory
- Correzione del rilevamento della codifica quando le variabili di ambiente delle impostazioni locali sono impostate in modo diverso
- Correzione di un arresto anomalo alla disconnessione con ripristino della connessione in corso
- Correzione del rilevamento del tempo di connessione
- Correzione del rilevamento errato dei socket chiusi
- Correzione di un'attesa infinita durante il tentativo di rilasciare un handle di istruzione durante il ripristino non riuscito
- Correzione del comportamento di disinstallazione non corretta quando entrambe le versioni 13 e 17 sono installate in Windows
- Correzione del comportamento di decrittografia sulla piattaforma Windows precedente (Windows 7, 8 e Server 2012)
- Correzione di un problema relativo alla cache quando si usa l'autenticazione ADAL in Windows
- Correzione di un problema che stava bloccando e sovrascrivendo i log di traccia in Windows

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd"></a>Correzioni di bug nel [!INCLUDE[msCoName](../../includes/msconame_md.md)] driver ODBC 17,1 per[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correzione di un ritardo di 1 secondo durante la chiamata di SQLFreeHandle con MARS abilitato e dell'attributo di connessione "Encrypt = Yes"
- Correzione di un errore 22003 arresto anomalo in SQLGetData Quando la dimensione del buffer passato è inferiore, i dati recuperati (Windows)
- Correzione dei messaggi di errore ADAL troncati
- Correzione di un bug raro in Windows a 32 bit durante la conversione di un numero a virgola mobile in un valore integer
- È stato risolto un problema per cui l'inserimento del valore Double nel campo Decimal con Always Encrypted on restituirebbe un errore di troncamento dei dati
- Correzione di un avviso nel programma di installazione di MacOS
- Correzione dell'invio dello stato errato a SQL Server durante il tentativo di ripristino della sessione quando sono abilitati la resilienza della connessione e il pool di connessioni, causando la rimozione della sessione dal server

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd"></a>Correzioni di bug in [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC driver 17 for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Correzione di un bug in cui quando si utilizza l'autenticazione Kerberos, BULK INSERT potrebbe non riuscire con l'errore "accesso negato"
- Soluzione alternativa rimossa per un bug unixODBC presente nella versione seguente 2.3.1 (driver raddoppiato le dimensioni di alcuni buffer passati a unixODBC)
- Correzione della resilienza della connessione (riconnessione) sospesa quando si usa ColumnEncryption = Enabled
- Correzione del bug di creazione del DSN, dove quando si usa l'opzione "Active Directory autenticazione interattiva", la finestra di autenticazione di Azure potrebbe non rispondere (Windows)
- Correzione di un arresto anomalo raro durante l'arresto di ODBC quando è abilitata l'esecuzione asincrona (si è verificato durante la cancellazione dell'handle
- È stato risolto un problema per cui il driver SQL causava un utilizzo elevato della CPU durante l'esecuzione di stored procedure lunghe
- Correzione dell'impossibilità di recuperare dati in una colonna varbinary (max) crittografata senza conversione
- È stato risolto un problema a causa del quale, dopo il recupero di una colonna crittografata con valori null (max) con SQLGetData () su un cursore statico, anche la colonna seguente viene annullata anche se contiene dati
- Correzione di un problema relativo al recupero del campo varbinary (max) con Always Encrypted
- Correzione di un problema di setlocale () che non funziona con Always Encrypted
- È stato risolto un problema relativo a SQLDescribeParam () che restituisce un errore quando viene chiamato sul parametro di stored procedure di tipo XML con Always Encrypted
- I caratteri di sottolineatura con escape corretti non funzionano in SQLTables
- Correzione di un bug in cui i dati ebraici (varchar) vengono troncati quando vengono restituiti come caratteri wide in Linux
- Correzione di un problema relativo all'esecuzione di query su char/varchar con codifica Shift-JIS da un'applicazione UTF-8
- Correzione del bug in cui la chiamata di SQLGetInfo con il parametro SQL_DRIVER_NAME ha restituito un nome file di tipo Linux in MacOS
- È stato risolto un problema per cui il caricamento dei dati di tipo carattere di Windows-1252, usando file di input di dimensioni maggiori di 32K byte nelle colonne VARCHAR usando l'utilità BCP causava errori
