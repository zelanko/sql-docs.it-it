---
description: Impostazione delle opzioni a livello di codice per il driver Paradox
title: Impostazione delle opzioni a livello di codice per il driver Paradox | Microsoft Docs
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
ms.openlocfilehash: 85b63df9e18b835c96bc0e59f7c937ece69f3999
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471573"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Impostazione delle opzioni a livello di codice per il driver Paradox

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Directory|Imposta la directory di destinazione.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Sequenza di fascicolazione|Sequenza in cui vengono ordinati i campi.<br /><br /> La sequenza può essere ASCII (impostazione predefinita), internazionale, svedese-finlandese o norvegese-danese.|Per impostare questa opzione in modo dinamico, usare la parola chiave **COLLATINGSEQUENCE** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Descrizione|Descrizione facoltativa dei dati nell'origine dati. ad esempio, "Data assunzione, cronologia stipendio e revisione corrente di tutti i dipendenti".|Per impostare questa opzione in modo dinamico, usare la parola chiave **Description** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Esclusivo|Se si seleziona la casella **esclusiva** , il database verrà aperto in modalità esclusiva ed è possibile accedervi da un solo utente alla volta. Le prestazioni sono migliorate durante l'esecuzione in modalità esclusiva.|Per impostare questa opzione in modo dinamico, usare la parola chiave **Exclusive** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Stile NET|Stile di accesso alla rete da usare per l'accesso ai dati Paradox: "3.*x*" per Paradox 3. *x* o "4. *x*"per Paradox 4. *x* o 5. *x*. Può essere impostato su "3. *x*"o" 4. *x*"se la versione è Paradox 4. *x* o 5. *x*; Se la versione è Paradox 3. *x*, lo stile deve essere "3. *x*".|Per impostare questa opzione in modo dinamico, usare la parola chiave **PARADOXNETSTYLE** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Timeout pagina|Specifica il periodo di tempo, in decimi di secondo, che una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Il valore predefinito è 600 decimi di secondo (60 secondi). Questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> Il timeout della pagina non può essere 0 a causa di un ritardo intrinseco. Il timeout della pagina non può essere inferiore al ritardo intrinseco, anche se l'opzione Timeout pagina è impostata al di sotto di tale valore.|Per impostare questa opzione in modo dinamico, usare la parola chiave **PAGETIMEOUT** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Sola lettura|Designa il database come di sola lettura.|Per impostare questa opzione in modo dinamico, usare la parola chiave **ReadOnly** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seleziona directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory contenente i file a cui si vuole accedere.<br /><br /> Quando si definisce una directory di origine dati, specificare la directory in cui si trovano i file usati più di frequente. Il driver ODBC utilizza questa directory come directory predefinita. Copiare altri file in questa directory se vengono usati di frequente. In alternativa, è possibile qualificare i nomi di file in un'istruzione SELECT con il nome della directory:<br /><br /> Seleziona \* da C:\MYDIR\EMP<br /><br /> In alternativa, è possibile specificare una nuova directory predefinita usando la funzione **SQLSetConnectOption** con l'opzione SQL_CURRENT_QUALIFIER.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seleziona directory di rete|Percorso completo della directory contenente un database di blocco di paradossi, perché contiene il file Pdoxusrs.net (in Paradox 4.* x*) o il file Paradox.NET (in Paradox 5.* x*). Se la directory non contiene uno di questi file, il driver Paradox ne crea uno. Per informazioni su questi file, vedere la documentazione di Paradox.<br /><br /> Prima di poter selezionare una directory di rete, è necessario immettere il nome utente Paradox nella casella di testo **nome utente** . Fare clic su **Seleziona directory di rete** per selezionare una directory di rete.|Per impostare questa opzione in modo dinamico, usare la parola chiave **PARADOXNETPATH** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Nome utente|Nome utente Paradox. Si tratta del nome visualizzato ad altri utenti di file Paradox quando viene rilevato un blocco.|Per impostare questa opzione in modo dinamico, usare la parola chiave **PARADOXUSERNAME** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
