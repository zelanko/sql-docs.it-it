---
description: SQLConfigDataSource (driver Access)
title: SQLConfigDataSource (driver Access) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: deb777e0d1d4a4e3ea9a45968256ad23dbeb56ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411987"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di accesso. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La funzione **SQLConfigDataSource** utilizzata per aggiungere, modificare o eliminare un'origine dati in modo dinamico utilizza le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|Sequenza in cui vengono ordinati i campi.<br /><br /> In questo modo viene impostata la stessa opzione della **sequenza di ordinamento** nella finestra di dialogo di installazione.|  
|COMPACT_DB|Esegue la compattazione dei dati in un file di database. Ha il formato seguente: COMPACT_DB =<path_name><optionaL_sort_order>\<optional ENCRYPT keyword> .<br /><br /> Quando si usa la parola chiave COMPACT_DB nella stessa istruzione con una parola chiave DSN, questo driver ignora la parola chiave DSN. La compattazione di un database e la specifica di un DSN sono pertanto un processo in due passaggi.|  
|CREATE_DB|Crea un file di database. Ha il formato seguente: CREATE_DB =<path_name><\<optional_sort-order> parola chiave optional_ENCRYPT, dove il nome del percorso è il percorso completo di un database di Microsoft Access. Se il nome del percorso specifica un database esistente, verrà restituito un errore. Il tipo di ordinamento sarà impostato nella finestra di dialogo nuovo database visualizzata quando si preme il pulsante Crea nella finestra di dialogo configurazione di Microsoft Access. Se non viene specificato alcun ordinamento, viene utilizzato General.<br /><br /> Quando si usa la parola chiave CREATE_DB nella stessa istruzione con una parola chiave DSN, questo driver ignora la parola chiave DSN. La creazione di un database e la specifica di un DSN sono pertanto un processo in due passaggi. Quando si usa la parola chiave CREATE_DB, se il percorso del database di Microsoft Access da creare contiene uno o più spazi, l'intero percorso deve essere racchiuso tra virgolette doppie, come illustrato negli esempi seguenti:<br /><br /> "C:\PROGRAMmi file comuni \ accesso. mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB = C:\TEMP\test.mdb (nessuna virgoletta necessaria)|  
|CREATE_SYSDB|Crea un file di database di sistema. Ha il formato seguente: CREATE_SYSDB = \<path-name> \<optional-sort-order> , dove il nome del percorso è il percorso completo di un database di Microsoft Access. Se il nome del percorso specifica un database esistente, verrà restituito un errore. Il tipo di ordinamento sarà impostato nella finestra di dialogo **nuovo database** visualizzata quando si fa clic sul pulsante **Crea** nella finestra di dialogo **configurazione di Microsoft Access ODBC** . Se non viene specificato alcun ordinamento, viene utilizzato General.|  
|CREATE_V2DB|Consente di creare un file di database compatibile con Microsoft Access 2,0. Ha il formato seguente: CREATE_V2DB = \<path-name> \<optional-sort-order> , dove il nome del percorso è il percorso completo di un database di Microsoft Access. Se il nome del percorso specifica un database esistente, verrà restituito un errore. Il tipo di ordinamento sarà impostato nella finestra di dialogo nuovo database visualizzata quando si preme il pulsante Crea nella finestra di dialogo configurazione di Microsoft Access. Se non viene specificato alcun ordinamento, viene utilizzato General.<br /><br /> Quando si usa la parola chiave CREATE_V2DB nella stessa istruzione con una parola chiave DSN, questo driver ignora la parola chiave DSN. La creazione di un database e la specifica di un DSN sono pertanto un processo in due passaggi.<br /><br /> Quando si usa la parola chiave CREATE_V2DB, se il percorso del database di Microsoft Access da creare contiene uno o più spazi, l'intero percorso deve essere racchiuso tra virgolette doppie, come illustrato negli esempi seguenti:<br /><br /> "C:\PROGRAMmi file comuni \ accesso. mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB = C:\TEMP\test.mdb (nessuna virgoletta necessaria)|  
|DBQ|Nome del file di database.<br /><br /> In questo modo viene impostata la stessa opzione del **database** nella finestra di dialogo di installazione.|  
|DEFAULTDIR|Specifica del percorso del file di database.|  
|DESCRIZIONE|Descrizione dei dati nell'origine dati.<br /><br /> Questa opzione consente di impostare la stessa opzione della **Descrizione** nella finestra di dialogo di installazione.|  
|DRIVER|Specifica del percorso per la DLL del driver.|  
|DRIVERID|ID di tipo integer per il driver.  25 (Microsoft Access)|  
|FIL|Tipo di file MS Access per Microsoft Access|  
|IMPLICITCOMMITSYNC|Determina se il driver Microsoft Access eseguirà commit interni o impliciti in modo asincrono. Questo valore inizialmente è impostato su "Sì", il che significa che il driver Microsoft Access attenderà il completamento dei commit in una transazione interna/implicita.<br /><br /> Il valore di questa opzione non deve essere modificato senza un'attenta considerazione delle conseguenze. Per ulteriori informazioni sull'opzione, vedere la *Guida per programmatori Microsoft Jet motore di database*.<br /><br /> Viene impostata la stessa opzione di **ImplicitCommitSync** nella finestra di dialogo di installazione.|  
|MAXBUFFERSIZE|Dimensioni del buffer interno, in kilobyte, utilizzate da Microsoft Access per trasferire dati da e verso il disco. Le dimensioni predefinite del buffer sono 2048 KB (visualizzate come 2048). È possibile usare qualsiasi valore intero divisibile per 256. Consente di impostare la stessa opzione della **dimensione del buffer** nella finestra di dialogo di installazione.|  
|MAXSCANROWS|Numero di righe da analizzare quando si imposta il tipo di dati di una colonna in base ai dati esistenti.<br /><br /> Per le righe da analizzare è possibile immettere un numero compreso tra 1 e 16. Il valore predefinito è 8. Se è impostato su 0, viene eseguita l'analisi di tutte le righe. (Un numero al di fuori del limite restituirà un errore).<br /><br /> Consente di impostare la stessa opzione delle **righe da analizzare** nella finestra di dialogo di installazione.|  
|PAGETIMEOUT|Specifica il periodo di tempo, in millisecondi, durante il quale una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Il valore predefinito è 5 decimi di secondo (0,5 secondi). Si noti che questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> In questo modo viene impostata la stessa opzione del **timeout della pagina** nella finestra di dialogo di installazione.|  
|PWD|Password.|  
|READONLY|TRUE per rendere di sola lettura il file; FALSE per fare in modo che il file non sia di sola lettura.<br /><br /> Viene impostata la stessa opzione di **sola lettura** nella finestra di dialogo di installazione.|  
|REPAIR_DB|Ripristina un database danneggiato da un errore che si verifica durante il processo di commit.<br /><br /> Quando si usa la parola chiave REPAIR_DB nella stessa istruzione con una parola chiave DSN, questo driver ignora la parola chiave DSN. Il ripristino di un database e la specifica di un DSN sono pertanto un processo in due passaggi.|  
|SYSTEMDB|Per il driver Microsoft Access, la specifica del percorso del file del database di sistema.<br /><br /> Viene impostata la stessa opzione del **database di sistema** nella finestra di dialogo di installazione.|  
|THREAD|Numero di thread in background per il motore da usare. Il valore predefinito è 3, ma può essere modificato.<br /><br /> Consente di impostare la stessa opzione dei **thread** nella finestra di dialogo di installazione.|  
|UID|Per il driver Microsoft Access, il nome dell'ID utente usato per l'accesso.|  
|USERCOMMITSYNC|Determina se il driver Microsoft Access eseguirà transazioni definite dall'utente in modo asincrono. Questo valore inizialmente è impostato su "Sì", il che significa che il driver Microsoft Access attenderà il completamento dei commit in una transazione definita dall'utente.<br /><br /> Il valore di questa opzione non deve essere modificato senza un'attenta considerazione delle conseguenze. Per ulteriori informazioni sull'opzione, vedere la *Guida per programmatori Microsoft Jet motore di database*.<br /><br /> Viene impostata la stessa opzione di **UserCommitSync** nella finestra di dialogo di installazione.|
