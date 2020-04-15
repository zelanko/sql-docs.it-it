---
title: Impostazione delle opzioni a livello di codice per il driver Paradox Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d04de1f0de4baca5b3f474ef9fbcf3f886e6906f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300761"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Impostazione delle opzioni a livello di codice per il driver Paradox

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Directory|Imposta la directory di destinazione.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Sequenza di confrontoCollating Sequence|Sequenza in cui vengono ordinati i campi.<br /><br /> La sequenza può essere ASCII (impostazione predefinita), internazionale, svedese-finlandese o norvegese-danese.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **COLLATINGSEQUENCE** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Descrizione|Descrizione facoltativa dei dati nell'origine dati. ad esempio, "Data di assunzione, cronologia degli stipendi e revisione corrente di tutti i dipendenti".|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DESCRIPTION** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Esclusivo|Se la casella **Esclusivo** è selezionata, il database verrà aperto in modalità Esclusiva ed è accessibile da un solo utente alla volta. Le prestazioni sono migliorate durante l'esecuzione in modalità esclusiva.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **EXCLUSIVE** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Stile rete|Stile di accesso alla rete da utilizzare quando si accede ai dati di Paradox: "3.*x"* per Paradox 3. *x* o "4. *x*" per Paradox 4. *x* o 5. *x*. Può essere impostato su "3. *x*" o "4. *x*" se la versione è Paradox 4. *x* o 5. *x*; se la versione è Paradox 3. *x*, lo stile deve essere "3. *x*".|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **PARADOXNETSTYLE** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Timeout pagina|Specifica il periodo di tempo, in decimi di secondo, in cui una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Il valore predefinito è 600 decimi di secondo (60 secondi). Questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> Il timeout della pagina non può essere 0 a causa di un ritardo intrinseco. Il timeout della pagina non può essere inferiore al ritardo intrinseco, anche se l'opzione di timeout della pagina è impostata al di sotto di tale valore.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **PAGETIMEOUT** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Sola lettura|Designa il database come di sola lettura.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **READONLY** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seleziona directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory contenente i file a cui si desidera accedere.<br /><br /> Quando si definisce una directory dell'origine dati, specificare la directory in cui si trovano i file utilizzati più di più di seguito. Il driver ODBC utilizza questa directory come directory predefinita. Copiare altri file in questa directory se vengono utilizzati di frequente. In alternativa, è possibile qualificare i nomi di file in un'istruzione SELECT con il nome della directory:<br /><br /> SELECT \* FROM:<br /><br /> In alternativa, è possibile specificare una nuova directory predefinita utilizzando la funzione **SQLSetConnectOption** con l'opzione SQL_CURRENT_QUALIFIER.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seleziona directory di rete|Il percorso completo della directory contenente un database di blocco di Paradox, perché contiene il file di Pdoxusrs.net (in Paradox 4.* x*) o il file Paradox.net (in Paradox 5.* x*). Se la directory non contiene uno di questi file, il driver Paradox ne crea uno. Per informazioni su questi file, vedere la documentazione di Paradox.For information about these files, see the Paradox documentation.<br /><br /> Prima di poter selezionare una directory di rete, è necessario immettere il proprio nome utente Paradox nella casella di testo **Nome utente.** Fare clic su **Seleziona directory di rete** per selezionare una directory di rete.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **PARADOXNETPATH** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Nome utente|Nome utente Paradox. Questo è il nome visualizzato ad altri utenti di file Paradox quando viene rilevato un blocco.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **PARADOXUSERNAME** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
