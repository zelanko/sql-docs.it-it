---
title: SQLConfigDataSource (Driver di accesso) Documenti Microsoft
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
ms.openlocfilehash: 48668525b578845fc330881d7c7de503d69d0928
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284051"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di accesso. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La funzione **SQLConfigDataSource** utilizzata per aggiungere, modificare o eliminare un'origine dati in modo dinamico utilizza le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|CONFRONTOSEQUENZA|Sequenza in cui vengono ordinati i campi.<br /><br /> In questo modo viene impostata la stessa opzione della sequenza di **fascicolazione** nella finestra di dialogo di impostazione.|  
|COMPACT_DB|Esegue la compattazione dei dati su un file di database. Ha il seguente formato: COMPACT_DB<\<path_name><optionaL_sort_order>> facoltativa della parola chiave ENCRYPT.<br /><br /> Quando si utilizza la parola chiave COMPACT_DB nella stessa istruzione con una parola chiave DSN, questo driver ignora la parola chiave DSN. Pertanto, la compattazione di un database e la specifica di un DSN è un processo in due passaggi.|  
|CREATE_DB|Crea un file di database. Ha il seguente formato: CREATE_DB \<<path_name>><in ordine optional_sort optional_ENCRYPT>, dove il nome del percorso è il percorso completo di un database di Microsoft Access. Se il nome del percorso specifica un database esistente, verrà restituito un errore. L'ordinamento sarà impostato nella finestra di dialogo Nuovo database quando si preme il pulsante Crea nella finestra di dialogo Installazione di Microsoft Access. Se non viene specificato alcun criterio di ordinamento, viene utilizzato Generale.<br /><br /> Quando si utilizza la parola chiave CREATE_DB nella stessa istruzione con una parola chiave DSN, questo driver ignora la parola chiave DSN. Pertanto, la creazione di un database e la specifica di un DSN è un processo in due passaggi. Quando si utilizza la parola chiave CREATE_DB, se il percorso del database di Microsoft Access da creare contiene uno o più spazi, l'intero nome del percorso deve essere racchiuso tra virgolette doppie, come illustrato negli esempi seguenti:<br /><br /> "C:"File DI PROGRAMMA"FILE COMMON"MyAccess.mdb"<br /><br /> "C:"FILE DI programma"Accesso2.mdb"<br /><br /> CREATE_DB : C: TEMP test.mdb (nessuna virgoletta necessaria)|  
|CREATE_SYSDB|Crea un file di database di sistema. Il formato è il\<seguente: \<CREATE_SYSDB nome-percorso>> facoltativo-sort-order, dove il nome del percorso è il percorso completo di un database di Microsoft Access. Se il nome del percorso specifica un database esistente, verrà restituito un errore. L'ordinamento sarà impostato nella finestra di dialogo **Nuovo database** quando si fa clic sul pulsante **Crea** nella finestra di dialogo Installazione ODBC di **Microsoft Access.** Se non viene specificato alcun criterio di ordinamento, viene utilizzato Generale.|  
|CREATE_V2DB|Crea un file di database compatibile con Microsoft Access 2.0. Il formato è il\<seguente: \<CREATE_V2DB nome-percorso>> facoltativo-sort-sort, dove il nome del percorso è il percorso completo di un database di Microsoft Access. Se il nome del percorso specifica un database esistente, verrà restituito un errore. L'ordinamento sarà impostato nella finestra di dialogo Nuovo database quando si preme il pulsante Crea nella finestra di dialogo Installazione di Microsoft Access. Se non viene specificato alcun criterio di ordinamento, viene utilizzato Generale.<br /><br /> Quando si utilizza la parola chiave CREATE_V2DB nella stessa istruzione con una parola chiave DSN, questo driver ignora la parola chiave DSN. Pertanto, la creazione di un database e la specifica di un DSN è un processo in due passaggi.<br /><br /> Quando si utilizza la parola chiave CREATE_V2DB, se il percorso del database di Microsoft Access da creare contiene uno o più spazi, l'intero nome del percorso deve essere racchiuso tra virgolette doppie, come illustrato negli esempi seguenti:<br /><br /> "C:"File DI PROGRAMMA"FILE COMMON"MyAccess.mdb"<br /><br /> "C:"FILE DI programma"Accesso2.mdb"<br /><br /> CREATE_V2DB: C: . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .|  
|DBQ|Nome del file di database.<br /><br /> In questo modo viene impostata la stessa opzione **Di Database** nella finestra di dialogo di installazione.|  
|DEFAULTDIR (DISE)|Specifica del percorso del file di database.|  
|DESCRIZIONE|Descrizione dei dati nell'origine dati.<br /><br /> In questo modo viene impostata la stessa opzione **Descrizione** nella finestra di dialogo di installazione.|  
|DRIVER|Specifica del percorso della DLL del driver.|  
|DRIVERID|Un ID intero per il driver.  25 (Microsoft Access)|  
|Fil|Tipo di file MS Access per Microsoft Access|  
|IMPLICITCOMMITSYNC|Determina se il driver di Microsoft Access eseguirà commit interni o impliciti in modo asincrono. Questo valore è inizialmente impostato su "Sì", il che significa che il driver di Microsoft Access attenderà il completamento dei commit in una transazione interna/implicita.<br /><br /> Il valore di questa opzione non deve essere modificato senza un'attenta considerazione delle conseguenze. Per ulteriori informazioni sull'opzione , vedere *Microsoft Jet Database Engine Programmer's Guide*.<br /><br /> In questo modo viene impostata la stessa opzione di **ImplicitCommitSync** nella finestra di dialogo di installazione.|  
|Maxbuffersize|Dimensione del buffer interno, in kilobyte, utilizzata da Microsoft Access per trasferire dati da e verso il disco. La dimensione predefinita del buffer è 2048 KB (visualizzato come 2048). È possibile utilizzare qualsiasi valore intero divisibile per 256.Any integer value divisible by 256 can be used. In questo modo viene impostata la stessa opzione **Di Dimensione buffer** nella finestra di dialogo di installazione.|  
|NUMERO MAXSCANROWS|Numero di righe da analizzare quando si imposta il tipo di dati di una colonna in base ai dati esistenti.<br /><br /> È possibile immettere un numero compreso tra 1 e 16 per le righe da scansionare. Il valore predefinito è 8; se è impostato su 0, vengono analizzate tutte le righe. (Un numero al di fuori del limite restituirà un errore.)<br /><br /> In questo modo viene impostata la stessa opzione **Righe da eseguire la scansione** nella finestra di dialogo di configurazione.|  
|Pagetimeout|Specifica il periodo di tempo, in millisecondi, durante il quale una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Il valore predefinito è cinque decimi di secondo (0,5 secondi). Si noti che questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> In questo modo viene impostata la stessa opzione di **Timeout pagina** nella finestra di dialogo di configurazione.|  
|PWD|Password.|  
|READONLY|TRUE per rendere il file di sola lettura; FALSE per rendere il file non di sola lettura.<br /><br /> In questo modo viene impostata la stessa opzione **Sola lettura** nella finestra di dialogo di installazione.|  
|REPAIR_DB|Ripristina un database danneggiato da un errore che si verifica durante il processo di commit.<br /><br /> Quando si utilizza la parola chiave REPAIR_DB nella stessa istruzione con una parola chiave DSN, questo driver ignora la parola chiave DSN. Pertanto, il ripristino di un database e la specifica di un DSN è un processo in due passaggi.|  
|SISTEMADB|Per il driver di Microsoft Access, la specifica del percorso del file di database di sistema.<br /><br /> In questo modo viene impostata la stessa opzione del **Database di** sistema nella finestra di dialogo di installazione.|  
|Discussioni|Numero di thread in background per il motore da utilizzare. Il valore predefinito è 3, ma può essere modificato.<br /><br /> In questo modo viene impostata la stessa opzione **di Thread** nella finestra di dialogo di installazione.|  
|UID|Per il driver di Microsoft Access, il nome dell'ID utente utilizzato per l'accesso.|  
|USERCOMMITSYNC (SINCRONIZZAZIONE UTENTE)|Determina se il driver di Microsoft Access eseguirà transazioni definite dall'utente in modo asincrono. Questo valore è inizialmente impostato su "Sì", il che significa che il driver di Microsoft Access attenderà il completamento dei commit in una transazione definita dall'utente.<br /><br /> Il valore di questa opzione non deve essere modificato senza un'attenta considerazione delle conseguenze. Per ulteriori informazioni sull'opzione , vedere *Microsoft Jet Database Engine Programmer's Guide*.<br /><br /> In questo modo viene impostata la stessa opzione di **UserCommitSync** nella finestra di dialogo di installazione.|
