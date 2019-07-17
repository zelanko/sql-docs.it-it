---
title: SQLConfigDataSource (Driver Paradox) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 33cc778d921b90a460dab6bda352fd7627d2cf7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054067"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (driver Paradox)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver Paradox. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il **SQLConfigDataSource** funzione che consente di aggiungere, modificare o eliminare un'origine dati utilizza in modo dinamico le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|La sequenza nella quale vengono ordinati i campi.<br /><br /> Quando viene usato il driver Paradox, la sequenza può essere ASCII (impostazione predefinita), internazionale, Finnish-Swedish o Danish-Norwegian.<br /><br /> Consente di impostare la stessa opzione come **sequenza di collazione** nella finestra di dialogo programma di installazione.|  
|DBQ|Il nome del file di database.<br /><br /> Consente di impostare la stessa opzione come **Database** nella finestra di dialogo programma di installazione.|  
|DEFAULTDIR|La specifica del percorso della directory.|  
|DESCRIPTION|Una descrizione dei dati nell'origine dati.<br /><br /> Consente di impostare la stessa opzione come **descrizione** nella finestra di dialogo programma di installazione.|  
|DRIVER|Specifica il percorso alla DLL del driver.|  
|DRIVERID|Un ID intero per il driver.<br /><br /> 26 (paradox 3.x)<br /><br /> 282 (paradox 4.x)<br /><br /> 538 (paradox 5.x)|  
|ESCLUSIVO|Determina se il database verrà aperto in modalità esclusiva (accessibili da un solo utente alla volta) o condiviso in modalità (accessibili da più di un utente alla volta). Può essere true (modalità esclusiva) o false (modalità condivisa).<br /><br /> Consente di impostare la stessa opzione come **esclusivo** nella finestra di dialogo programma di installazione.|  
|FIL|Tipo Paradox file 3.x, Paradox 4.x o Paradox 5.x|  
|FILETYPE|Tipo di file per il driver di testo (testo).|  
|PAGETIMEOUT|Specifica il periodo di tempo, in decimi di secondo, che una pagina, se non utilizzato, rimane nel buffer prima della rimozione. Il valore predefinito è 600 decimi di secondo (60 secondi). Si noti che questa opzione si applica a tutte le origini dati che usano il driver ODBC.<br /><br /> Consente di impostare la stessa opzione come **Page Timeout** nella finestra di dialogo programma di installazione.|  
|PARADOXNETPATH|Il percorso completo della directory contenente un database di blocco Paradox, perché contiene il file PDOXUSRS.net (4, Paradox. *x*) o il file PARADOX.net (5, Paradox. *x*). Se la directory non contiene uno di questi file, il driver Paradox crea uno. Per informazioni su questi file, vedere la documentazione Paradox.<br /><br /> Prima di una directory di rete può essere selezionata, è necessario specificare un nome utente Paradox.<br /><br /> Consente di impostare la stessa opzione come **Directory di rete selezionare** nella finestra di dialogo programma di installazione.|  
|PARADOXNETSTYLE|Per il driver Paradox, nella rete accesso stile da utilizzare per l'accesso ai dati Paradox: entrambi "3.x" per Paradox 3. *x* o "4.x" per Paradox 4. *x* o 5. *x*. Può essere impostare su "3.x" o "4.x" se la versione è 4 Paradox. *x* o 5. *x*; se la versione è 3 Paradox. *x*, lo stile deve essere "3".<br /><br /> Consente di impostare la stessa opzione come **stile Net** nella finestra di dialogo programma di installazione.|  
|PARADOXUSERNAME|Per il driver Paradox, il nome utente Paradox.<br /><br /> Consente di impostare la stessa opzione come **nome utente** nella finestra di dialogo programma di installazione.|  
|PWD|Password.<br /><br /> Questa parola chiave facoltativa e non verrà mai scritto nel file dal driver. Viene usato in una chiamata a **SQLDriverConnect** sui file Paradox protette con password. La password utilizzata sarà valida ogni volta che viene aperta una tabella. Se nessuna password viene passata nella stringa di connessione, non viene stabilita alcuna password per tale tabella. Se le tabelle contengono password diverse, più può essere aperto nella stessa sessione, né possono essere unite le tabelle.|  
|READONLY|TRUE per rendere i file di sola lettura. FALSE per rendere i file non di sola lettura.<br /><br /> Consente di impostare la stessa opzione come **Read Only** nella finestra di dialogo programma di installazione.|  
|THREAD|Il numero di thread in background per il motore da usare. Questo valore è 3 e non può essere modificato.<br /><br /> Consente di impostare la stessa opzione come **thread** nella finestra di dialogo programma di installazione.|
