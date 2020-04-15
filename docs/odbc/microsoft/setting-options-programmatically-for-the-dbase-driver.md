---
title: Impostazione delle opzioni a livello di codice per il driver dBASE Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75889d9ff3ccfe01f9b8d5141df7774205522815
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300781"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>Impostazione delle opzioni a livello di codice per il driver dBASE

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Conteggio righe approssimativo|Determina se le statistiche sulle dimensioni della tabella sono approssimate. Questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **STATISTICS** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Sequenza di confrontoCollating Sequence|Sequenza in cui vengono ordinati i campi.<br /><br /> La sequenza può essere: ASCII (impostazione predefinita) o internazionale.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **COLLATINGSEQUENCE** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Data Source Name|Nome che identifica l'origine dati, ad esempio Retribuzioni o Personale.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DSN** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Database|È possibile impostare un'origine dati di Microsoft Access senza selezionare o creare un database. Se al momento dell'installazione non viene fornito alcun database, agli utenti verrà richiesto di selezionare un file di database quando si connettono all'origine dati.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DBQ** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Descrizione|Descrizione facoltativa dei dati nell'origine dati. ad esempio, "Data di assunzione, cronologia degli stipendi e revisione corrente di tutti i dipendenti".|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DESCRIPTION** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Esclusivo|Se la casella **Esclusivo** è selezionata, il database verrà aperto in modalità Esclusiva ed è accessibile da un solo utente alla volta. Le prestazioni vengono migliorate quando viene eseguito in modalità esclusiva.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **EXCLUSIVE** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Timeout pagina|Specifica il periodo di tempo, in decimi di secondo, in cui una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Il valore predefinito è 600 decimi di secondo (60 secondi). Questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> Il timeout della pagina non può essere 0 a causa di un ritardo intrinseco. Il timeout della pagina non può essere inferiore al ritardo intrinseco, anche se l'opzione di timeout della pagina è impostata al di sotto di tale valore.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **PAGETIMEOUT** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Sola lettura|Designa il database come di sola lettura.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **READONLY** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Seleziona directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory contenente i file a cui si desidera accedere.<br /><br /> Quando si definisce una directory dell'origine dati, specificare la directory in cui si trovano i file utilizzati più di frequente. Il driver ODBC utilizza questa directory come directory predefinita. Copiare altri file in questa directory se vengono utilizzati di frequente. In alternativa, è possibile qualificare i nomi di file in un'istruzione SELECT con il nome della directory:<br /><br /> SELECT \* FROM:<br /><br /> In alternativa, è possibile specificare una nuova directory predefinita utilizzando la funzione **SQLSetConnectOption** con l'opzione SQL_CURRENT_QUALIFIER.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Mostra righe eliminate|Specifica se le righe contrassegnate come eliminate possono essere recuperate o posizionate. Se l'opzione è deselezionata, le righe eliminate non vengono visualizzate; se selezionata, le righe eliminate vengono considerate come le righe non eliminate. Per impostazione predefinita, l'opzione è deselezionata.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DELETED** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|
