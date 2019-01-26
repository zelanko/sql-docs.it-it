---
title: Impostazione delle opzioni a livello di codice per il Driver Paradox | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd92344552371e2e052a958485340b70522cc121
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044517"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Impostazione delle opzioni a livello di codice per il driver Paradox

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Directory|Imposta la directory di destinazione.|Per impostare questa opzione in modo dinamico, usare il **DEFAULTDIR** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Sequenza di ordinamento|La sequenza nella quale vengono ordinati i campi.<br /><br /> La sequenza può essere ASCII (predefinito), internazionale, Finnish-Swedish o Danish-Norwegian.|Per impostare questa opzione in modo dinamico, usare il **COLLATINGSEQUENCE** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Descrizione|Una descrizione facoltativa dei dati nell'origine dati; ad esempio, "Hire data, cronologia degli stipendi e situazione corrente di tutti i dipendenti."|Per impostare questa opzione in modo dinamico, usare il **DESCRIPTION** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Exclusive|Se il **esclusivo** casella è selezionata, il database verrà aperto in modalità esclusiva e sono accessibili da un solo utente alla volta. Le prestazioni sono ottimizzate durante l'esecuzione in modalità esclusiva.|Per impostare questa opzione in modo dinamico, usare il **esclusivo** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Stile NET|Il tipo di accesso di rete da utilizzare per l'accesso ai dati Paradox: entrambi "3.*x*" per Paradox 3. *x* o "4. *x*"per Paradox 4. *x* o 5. *x*. Può essere impostato su "3. *x*"o" 4. *x*"se la versione 4 Paradox. *x* o 5. *x*; se la versione è 3 Paradox. *x*, lo stile deve essere "3. *x*".|Per impostare questa opzione in modo dinamico, usare il **PARADOXNETSTYLE** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Timeout di pagina|Specifica il periodo di tempo, in decimi di secondo, che una pagina, se non utilizzato, rimane nel buffer prima della rimozione. Il valore predefinito è 600 decimi di secondo (60 secondi). Questa opzione si applica a tutte le origini dati che usano il driver ODBC.<br /><br /> Il timeout della pagina non può essere 0 a causa di un ritardo inerente. Il timeout della pagina non può essere minore del ritardo inerente, anche se è impostata l'opzione di timeout della pagina di sotto di tale valore.|Per impostare questa opzione in modo dinamico, usare il **PAGETIMEOUT** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Read Only|Definisce il database in sola lettura.|Per impostare questa opzione in modo dinamico, usare il **READONLY** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Selezionare la Directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory che contiene i file che si desidera accedere.<br /><br /> Quando la definizione di una directory di origine dati specifica la directory in cui la più comunemente usati i file si trovano. Il driver ODBC usa tale directory come directory predefinita. Copiare altri file in questa directory, se vengono usati frequentemente. In alternativa, è possibile qualificare nomi di file in un'istruzione SELECT con il nome della directory:<br /><br /> SELEZIONARE \* DA C:\MYDIR\EMP<br /><br /> Oppure, è possibile specificare una nuova directory predefinita usando il **SQLSetConnectOption** canonica con l'opzione SQL_CURRENT_QUALIFIER.|Per impostare questa opzione in modo dinamico, usare il **DEFAULTDIR** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Selezionare la Directory di rete|Il percorso completo della directory contenente un database di blocco Paradox, perché contiene il file Pdoxusrs.net (4, Paradox. *x*) o il file Paradox.net (5, Paradox. *x*). Se la directory non contiene uno di questi file, il driver Paradox crea uno. Per informazioni su questi file, vedere la documentazione Paradox.<br /><br /> Prima di poter selezionare una directory di rete, è necessario immettere il nome utente Paradox nel **nome utente** casella di testo. Fare clic su **Directory di rete selezionare** per selezionare una directory di rete.|Per impostare questa opzione in modo dinamico, usare il **PARADOXNETPATH** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Nome utente|Il nome utente Paradox. Si tratta del nome visualizzato agli altri utenti di file Paradox quando viene incontrato un blocco.|Per impostare questa opzione in modo dinamico, usare il **PARADOXUSERNAME** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
