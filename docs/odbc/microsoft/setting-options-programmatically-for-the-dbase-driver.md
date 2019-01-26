---
title: Impostazione opzioni a livello di codice per il Driver dBASE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a268e72262f9f8252ea89774876f3d04008fe4c4
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044437"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>Impostazione delle opzioni a livello di codice per il driver dBASE

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Conteggio righe approssimative|Determina se le statistiche delle tabelle delle dimensioni sono approssimative. Questa opzione si applica a tutte le origini dati che usano il driver ODBC.|Per impostare questa opzione in modo dinamico, usare il **statistiche** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Sequenza di ordinamento|La sequenza nella quale vengono ordinati i campi.<br /><br /> La sequenza può essere: ASCII (predefinito) o internazionale.|Per impostare questa opzione in modo dinamico, usare il **COLLATINGSEQUENCE** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Nome origine dati|Un nome che identifica l'origine dati, ad esempio Payroll o personale.|Per impostare questa opzione in modo dinamico, usare il **DSN** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Database|Un'origine dati Microsoft Access da impostare senza selezionare o creare un database. Se viene specificato alcun database al momento dell'installazione, gli utenti verranno richiesto di selezionare un file di database al momento della connessione all'origine dati.|Per impostare questa opzione in modo dinamico, usare il **DBQ** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Descrizione|Una descrizione facoltativa dei dati nell'origine dati; ad esempio, "Hire data, cronologia degli stipendi e situazione corrente di tutti i dipendenti."|Per impostare questa opzione in modo dinamico, usare il **DESCRIPTION** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Exclusive|Se il **esclusivo** casella è selezionata, il database verrà aperto in modalità esclusiva e sono accessibili da un solo utente alla volta. Le prestazioni risultano migliorate quando è in esecuzione in modalità esclusiva.|Per impostare questa opzione in modo dinamico, usare il **esclusivo** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Timeout di pagina|Specifica il periodo di tempo, in decimi di secondo, che una pagina, se non utilizzato, rimane nel buffer prima che venga rimosso. Il valore predefinito è 600 decimi di secondo (60 secondi). Questa opzione si applica a tutte le origini dati che usano il driver ODBC.<br /><br /> Il timeout della pagina non può essere 0 a causa di un ritardo inerente. Il timeout della pagina non può essere minore del ritardo inerente, anche se è impostata l'opzione di timeout della pagina di sotto di tale valore.|Per impostare questa opzione in modo dinamico, usare il **PAGETIMEOUT** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Read Only|Definisce il database in sola lettura.|Per impostare questa opzione in modo dinamico, usare il **READONLY** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Selezionare la Directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory che contiene i file che si desidera accedere.<br /><br /> Quando si definisce una directory di origine dati, specificare la directory in cui si trovano i file usati più di frequente. Il driver ODBC usa tale directory come directory predefinita. Copiare altri file in questa directory, se vengono usati frequentemente. In alternativa, è possibile qualificare nomi di file in un'istruzione SELECT con il nome della directory:<br /><br /> SELEZIONARE \* DA C:\MYDIR\EMP<br /><br /> Oppure, è possibile specificare una nuova directory predefinita usando il **SQLSetConnectOption** canonica con l'opzione SQL_CURRENT_QUALIFIER.|Per impostare questa opzione in modo dinamico, usare il **DEFAULTDIR** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Mostra le righe eliminate|Specifica se le righe che sono state contrassegnate come eliminati possono essere recuperate o posizionato in corrispondenza. Se deselezionata, le righe eliminate non vengono visualizzate; Se selezionata, le righe eliminate vengono considerate lo stesso come righe non è stato eliminato. Per impostazione predefinita, l'opzione è deselezionata.|Per impostare questa opzione in modo dinamico, usare il **DELETED** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|
