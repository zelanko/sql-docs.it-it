---
title: SQLConfigDataSource (driver Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68e60d7ca9c37865c1b265297d24591638a44965
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283931"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (driver Paradox)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver Paradox. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La funzione **SQLConfigDataSource** utilizzata per aggiungere, modificare o eliminare un'origine dati in modo dinamico utilizza le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|Sequenza in cui vengono ordinati i campi.<br /><br /> Quando si usa il driver Paradox, la sequenza può essere ASCII (impostazione predefinita), internazionale, svedese-finlandese o norvegese-danese.<br /><br /> In questo modo viene impostata la stessa opzione della **sequenza di ordinamento** nella finestra di dialogo di installazione.|  
|DBQ|Nome del file di database.<br /><br /> In questo modo viene impostata la stessa opzione del **database** nella finestra di dialogo di installazione.|  
|DEFAULTDIR|Specifica del percorso della directory.|  
|DESCRIZIONE|Descrizione dei dati nell'origine dati.<br /><br /> Questa opzione consente di impostare la stessa opzione della **Descrizione** nella finestra di dialogo di installazione.|  
|DRIVER|Specifica del percorso per la DLL del driver.|  
|DRIVERID|ID di tipo integer per il driver.<br /><br /> 26 (Paradox 3. x)<br /><br /> 282 (Paradox 4. x)<br /><br /> 538 (Paradox 5. x)|  
|ESCLUSIVO|Determina se il database verrà aperto in modalità esclusiva (accessibile da un solo utente alla volta) o in modalità condivisa (a cui si accede da più utenti alla volta). Può essere true (modalità esclusiva) o false (modalità condivisa).<br /><br /> Questa opzione consente di impostare la stessa opzione come **esclusiva** nella finestra di dialogo di installazione.|  
|FIL|Tipo di file Paradox 3. x, Paradox 4. x o Paradox 5. x|  
|FILETYPE|Tipo di file per il driver di testo (testo).|  
|PAGETIMEOUT|Specifica il periodo di tempo, in decimi di secondo, che una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Il valore predefinito è 600 decimi di secondo (60 secondi). Si noti che questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> In questo modo viene impostata la stessa opzione del **timeout della pagina** nella finestra di dialogo di installazione.|  
|PARADOXNETPATH|Percorso completo della directory contenente un database di blocco di paradossi, perché contiene il file PDOXUSRS.net (in Paradox 4.* x*) o il file Paradox.NET (in Paradox 5.* x*). Se la directory non contiene uno di questi file, il driver Paradox ne crea uno. Per informazioni su questi file, vedere la documentazione di Paradox.<br /><br /> Prima di poter selezionare una directory di rete, è necessario immettere un nome utente Paradox.<br /><br /> Consente di impostare la stessa opzione di **Seleziona directory di rete** nella finestra di dialogo di installazione.|  
|PARADOXNETSTYLE|Per il driver Paradox, lo stile di accesso alla rete da usare per l'accesso ai dati Paradox: "3. x" per Paradox 3. *x* o "4. x" per Paradox 4. *x* o 5. *x*. Può essere impostato su "3. x" o "4. x" se la versione è Paradox 4. *x* o 5. *x*; Se la versione è Paradox 3. *x*, lo stile deve essere "3. x".<br /><br /> In questo modo viene impostata la stessa opzione di **net Style** nella finestra di dialogo di installazione.|  
|PARADOXUSERNAME|Per il driver Paradox, il nome utente Paradox.<br /><br /> In questo modo, la stessa opzione del **nome utente** viene impostata nella finestra di dialogo di installazione.|  
|PWD|Password.<br /><br /> Si tratta di una parola chiave facoltativa che non verrà mai scritta nel file dal driver. Viene usato in una chiamata a **SQLDriverConnect** per i file Paradox protetti da password. La password utilizzata sarà valida ogni volta che viene aperta una tabella. Se nella stringa di connessione non viene passata alcuna password, non viene stabilita alcuna password per tale tabella. Se le tabelle hanno password diverse, non è possibile aprire più di una sessione nella stessa sessione né unire in join le tabelle.|  
|READONLY|TRUE per rendere di sola lettura il file; FALSE per fare in modo che il file non sia di sola lettura.<br /><br /> Viene impostata la stessa opzione di **sola lettura** nella finestra di dialogo di installazione.|  
|THREAD|Numero di thread in background per il motore da usare. Questo valore è 3 e non può essere modificato.<br /><br /> Consente di impostare la stessa opzione dei **thread** nella finestra di dialogo di installazione.|
