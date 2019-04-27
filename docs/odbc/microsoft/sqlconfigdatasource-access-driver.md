---
title: SQLConfigDataSource (Access Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd626d476bf1c4ac8b4f83f397584c367299904f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62665406"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni di accesso specifici del Driver. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il **SQLConfigDataSource** funzione che consente di aggiungere, modificare o eliminare un'origine dati utilizza in modo dinamico le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|La sequenza nella quale vengono ordinati i campi.<br /><br /> Consente di impostare la stessa opzione come **sequenza di collazione** nella finestra di dialogo programma di installazione.|  
|COMPACT_DB|Esegue la compattazione dei dati in un file di database. Ha il formato seguente: COMPACT_DB = < nome_percorso >< optionaL_sort_order >\<parola chiave facoltativa ENCRYPT >.<br /><br /> Quando si usa la parola chiave COMPACT_DB nella stessa istruzione con una parola chiave DSN, il driver ignora la parola chiave DSN. Pertanto, la compattazione di un database e specificando un DSN è un processo in due passaggi.|  
|CREATE_DB|Crea un file di database. Ha il formato seguente: CREATE_DB = < nome_percorso >\<optional_sort ordine >< optional_ENCRYPT parola chiave >, dove il nome del percorso è il percorso completo di un database Microsoft Access. Verrà restituito un errore se il nome di percorso specifica un database esistente. L'ordinamento sarà come set di backup nella finestra di dialogo Nuovo Database visualizzato quando viene premuto il pulsante Crea nella finestra di dialogo Configurazione dell'accesso Microsoft. Se viene specificato alcun ordinamento, viene utilizzato generale.<br /><br /> Quando si usa la parola chiave CREATE_DB nella stessa istruzione con una parola chiave DSN, il driver ignora la parola chiave DSN. Pertanto, la creazione di un database e specificando un DSN è un processo in due passaggi. Quando si usa la parola chiave CREATE_DB, se il nome del percorso del database Microsoft Access deve essere creato contiene uno o più spazi, quindi l'intero percorso deve essere delimitata da virgolette doppie, come illustrato negli esempi seguenti:<br /><br /> "C:\PROGRAM FILES\COMMON Files \ MyAccess.mdb"<br /><br /> "C:\Programmi\Microsoft FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb (virgolette non necessite)|  
|CREATE_SYSDB|Crea un file di database di sistema. Ha il formato seguente: CREATE_SYSDB =\<percorso-name >\<facoltativo-ordinamento >, dove il nome del percorso è il percorso completo di un database Microsoft Access. Verrà restituito un errore se il nome di percorso specifica un database esistente. L'ordinamento verrà impostato nel **Nuovo Database** visualizzata la finestra di dialogo quando il **Create** si fa clic sul pulsante nel **configurazione dell'accesso Microsoft ODBC** nella finestra di dialogo. Se viene specificato alcun ordinamento, viene utilizzato generale.|  
|CREATE_V2DB|Crea un file di database che è compatibile con Microsoft Access 2.0. Ha il formato seguente: CREATE_V2DB =\<percorso-name >\<facoltativo-ordinamento >, dove il nome del percorso è il percorso completo di un database Microsoft Access. Verrà restituito un errore se il nome di percorso specifica un database esistente. L'ordinamento sarà come set di backup nella finestra di dialogo Nuovo Database visualizzato quando viene premuto il pulsante Crea nella finestra di dialogo Configurazione dell'accesso Microsoft. Se viene specificato alcun ordinamento, viene utilizzato generale.<br /><br /> Quando si usa la parola chiave CREATE_V2DB nella stessa istruzione con una parola chiave DSN, il driver ignora la parola chiave DSN. Pertanto, la creazione di un database e specificando un DSN è un processo in due passaggi.<br /><br /> Quando si usa la parola chiave CREATE_V2DB, se il nome del percorso del database Microsoft Access deve essere creato contiene uno o più spazi, quindi l'intero percorso deve essere delimitata da virgolette doppie, come illustrato negli esempi seguenti:<br /><br /> "C:\PROGRAM FILES\COMMON Files \ MyAccess.mdb"<br /><br /> "C:\Programmi\Microsoft FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb (virgolette non necessite)|  
|DBQ|Il nome del file di database.<br /><br /> Consente di impostare la stessa opzione come **Database** nella finestra di dialogo programma di installazione.|  
|DEFAULTDIR|Specifica il percorso al file di database.|  
|DESCRIPTION|Una descrizione dei dati nell'origine dati.<br /><br /> Consente di impostare la stessa opzione come **descrizione** nella finestra di dialogo programma di installazione.|  
|DRIVER|Specifica il percorso alla DLL del driver.|  
|DRIVERID|Un ID intero per il driver.  25 (Microsoft Access)|  
|FIL|Tipo di accesso MS per l'accesso a Microsoft di file|  
|IMPLICITCOMMITSYNC|Determina se il driver Microsoft Access verrà eseguite commit interni o implicite in modo asincrono. Questo valore è inizialmente impostato su "Sì", il che significa che il driver Microsoft Access rimarrà in attesa per i commit in una transazione interna/implicita per essere completati.<br /><br /> Il valore di questa opzione non deve essere modificato senza un'attenta valutazione delle conseguenze. Per altre informazioni sull'opzione, vedere la *Guida per programmatori di Microsoft Jet Database Engine*.<br /><br /> Consente di impostare la stessa opzione come **ImplicitCommitSync** nella finestra di dialogo programma di installazione.|  
|MAXBUFFERSIZE|Le dimensioni del buffer interno, espressa in kilobyte, che viene utilizzata da Microsoft Access per trasferire i dati da e verso il disco. Le dimensioni del buffer predefinita sono 2048 KB (visualizzato come 2048). Numeri interi divisibili per 256 utilizzabile. Consente di impostare la stessa opzione come **le dimensioni del Buffer** nella finestra di dialogo programma di installazione.|  
|MAXSCANROWS|Il numero di righe da analizzare quando si imposta il tipo di dati di una colonna in base ai dati esistenti.<br /><br /> È possibile immettere un numero da 1 a 16 per le righe da analizzare. Il valore predefinito è 8, mentre Se è impostato su 0, vengono analizzate tutte le righe. (Un numero di fuori del limite verrà restituito un errore).<br /><br /> Consente di impostare la stessa opzione come **righe da analizzare** nella finestra di dialogo programma di installazione.|  
|PAGETIMEOUT|Specifica il periodo di tempo, espresso in millisecondi, che una pagina, se non utilizzato, rimane nel buffer prima della rimozione. Il valore predefinito è cinque-decimi di secondo (0,5 secondi). Si noti che questa opzione si applica a tutte le origini dati che usano il driver ODBC.<br /><br /> Consente di impostare la stessa opzione come **Page Timeout** nella finestra di dialogo programma di installazione.|  
|PWD|Password.|  
|READONLY|TRUE per rendere i file di sola lettura. FALSE per rendere i file non di sola lettura.<br /><br /> Consente di impostare la stessa opzione come **Read Only** nella finestra di dialogo programma di installazione.|  
|REPAIR_DB|Consente di ripristinare un database danneggiato a causa di un errore che si verifica durante il processo di commit.<br /><br /> Quando si usa la parola chiave REPAIR_DB nella stessa istruzione con una parola chiave DSN, il driver ignora la parola chiave DSN. Pertanto, tentare di ripristinare un database e specificando un DSN è un processo in due passaggi.|  
|SYSTEMDB|Per il driver Microsoft Access, la specifica del percorso al file di database di sistema.<br /><br /> Consente di impostare la stessa opzione come **Database di sistema** nella finestra di dialogo programma di installazione.|  
|THREAD|Il numero di thread in background per il motore da usare. Questo valore predefinito è 3, ma può essere modificato.<br /><br /> Consente di impostare la stessa opzione come **thread** nella finestra di dialogo programma di installazione.|  
|UID|Per il driver Microsoft Access, il nome dell'ID utente utilizzato per l'accesso.|  
|USERCOMMITSYNC|Determina se il driver Microsoft Access verrà eseguite in modo asincrono le transazioni definite dall'utente. Questo valore è inizialmente impostato su "Sì", il che significa che il driver Microsoft Access rimarrà in attesa per i commit in una transazione definita dall'utente per il completamento.<br /><br /> Il valore di questa opzione non deve essere modificato senza un'attenta valutazione delle conseguenze. Per altre informazioni sull'opzione, vedere la *Guida per programmatori di Microsoft Jet Database Engine*.<br /><br /> Consente di impostare la stessa opzione come **UserCommitSync** nella finestra di dialogo programma di installazione.|
