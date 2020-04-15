---
title: SQLConfigDataSource (Driver Di Paradox) Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283931"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (driver Paradox)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver Paradox.This topic provides Paradox Driver-specific information. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La funzione **SQLConfigDataSource** utilizzata per aggiungere, modificare o eliminare un'origine dati in modo dinamico utilizza le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|CONFRONTOSEQUENZA|Sequenza in cui vengono ordinati i campi.<br /><br /> Quando si utilizza il driver Paradox, la sequenza può essere ASCII (impostazione predefinita), internazionale, svedese-finlandese o norvegese-danese.<br /><br /> In questo modo viene impostata la stessa opzione della sequenza di **fascicolazione** nella finestra di dialogo di impostazione.|  
|DBQ|Nome del file di database.<br /><br /> In questo modo viene impostata la stessa opzione **Di Database** nella finestra di dialogo di installazione.|  
|DEFAULTDIR (DISE)|Specifica del percorso della directory.|  
|DESCRIZIONE|Descrizione dei dati nell'origine dati.<br /><br /> In questo modo viene impostata la stessa opzione **Descrizione** nella finestra di dialogo di installazione.|  
|DRIVER|Specifica del percorso della DLL del driver.|  
|DRIVERID|Un ID intero per il driver.<br /><br /> 26 (Paradosso 3.x)<br /><br /> 282 (Paradosso 4.x)<br /><br /> 538 (Paradosso 5.x)|  
|Esclusivo|Determina se il database verrà aperto in modalità esclusiva (accessibile da un solo utente alla volta) o in modalità condivisa (accessibile da più di un utente alla volta). Può essere true (modalità esclusiva) o false (modalità condivisa).<br /><br /> In questo modo viene impostata la stessa opzione **Esclusivo** nella finestra di dialogo di installazione.|  
|Fil|Tipo di file Paradox 3.x, Paradox 4.x o Paradox 5.x|  
|Filetype|Tipo di file per il driver di testo (testo).|  
|Pagetimeout|Specifica il periodo di tempo, in decimi di secondo, in cui una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Il valore predefinito è 600 decimi di secondo (60 secondi). Si noti che questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> In questo modo viene impostata la stessa opzione di **Timeout pagina** nella finestra di dialogo di configurazione.|  
|Paradoxnetpath|Il percorso completo della directory contenente un database di blocco di Paradox, perché contiene il file PDOXUSRS.net (in Paradox 4.* x*) o il file PARADOX.net (in Paradox 5.* x*). Se la directory non contiene uno di questi file, il driver Paradox ne crea uno. Per informazioni su questi file, vedere la documentazione di Paradox.For information about these files, see the Paradox documentation.<br /><br /> Prima di poter selezionare una directory di rete, è necessario immettere un nome utente Paradox.<br /><br /> In questo modo viene impostata la stessa opzione **di Seleziona directory di rete** nella finestra di dialogo di installazione.|  
|PARADOXNETSTYLE|Per il driver Paradox, lo stile di accesso alla rete da utilizzare per l'accesso ai dati di Paradox: "3.x" per Paradox 3. *x* o "4.x" per Paradox 4. *x* o 5. *x*. Può essere impostato su "3.x" o "4.x" se la versione è Paradox 4. *x* o 5. *x*; se la versione è Paradox 3. *x*, lo stile deve essere "3.x".<br /><br /> In questo modo viene impostata la stessa opzione di **Stile di rete** nella finestra di dialogo di impostazione.|  
|PARADOXNOMEUTENTE|Per il driver Paradox, il nome utente Paradox.<br /><br /> In questo modo viene impostata la stessa opzione **di Nome utente** nella finestra di dialogo di installazione.|  
|PWD|Password.<br /><br /> Si tratta di una parola chiave facoltativa che non verrà mai scritta nel file dal driver. Viene utilizzato in una chiamata a **SQLDriverConnect** contro i file Paradox protetti da password. La password utilizzata sarà valida ogni volta che viene aperta una tabella. Se nella stringa di connessione non viene passata alcuna password, non viene stabilita alcuna password per tale tabella. Se le tabelle hanno password diverse, non è possibile aprirle più di una nella stessa sessione, né le tabelle possono essere unite in join.|  
|READONLY|TRUE per rendere il file di sola lettura; FALSE per rendere il file non di sola lettura.<br /><br /> In questo modo viene impostata la stessa opzione **Sola lettura** nella finestra di dialogo di installazione.|  
|Discussioni|Numero di thread in background per il motore da utilizzare. Questo valore è 3 e non può essere modificato.<br /><br /> In questo modo viene impostata la stessa opzione **di Thread** nella finestra di dialogo di installazione.|
