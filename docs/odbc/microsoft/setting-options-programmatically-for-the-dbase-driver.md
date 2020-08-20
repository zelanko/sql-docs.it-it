---
description: Impostazione delle opzioni a livello di codice per il driver dBASE
title: Impostazione delle opzioni a livello di codice per il driver dBASE | Microsoft Docs
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
ms.openlocfilehash: 7c4b86b8284ca9a47e3ad40b1680a362035a3f13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471583"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>Impostazione delle opzioni a livello di codice per il driver dBASE

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Conteggio delle righe approssimativo|Determina se le statistiche sulle dimensioni della tabella sono approssimate. Questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.|Per impostare questa opzione in modo dinamico, usare la parola chiave **Statistics** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Sequenza di fascicolazione|Sequenza in cui vengono ordinati i campi.<br /><br /> La sequenza può essere: ASCII (impostazione predefinita) o internazionale.|Per impostare questa opzione in modo dinamico, usare la parola chiave **COLLATINGSEQUENCE** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Data Source Name|Nome che identifica l'origine dati, ad esempio Payroll o personale.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DSN** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Database|Un'origine dati di Microsoft Access può essere configurata senza selezionare o creare un database. Se non viene fornito alcun database durante l'installazione, agli utenti verrà richiesto di selezionare un file di database quando si connettono all'origine dati.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DBQ** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Descrizione|Descrizione facoltativa dei dati nell'origine dati. ad esempio, "Data assunzione, cronologia stipendio e revisione corrente di tutti i dipendenti".|Per impostare questa opzione in modo dinamico, usare la parola chiave **Description** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Esclusivo|Se si seleziona la casella **esclusiva** , il database verrà aperto in modalità esclusiva ed è possibile accedervi da un solo utente alla volta. Le prestazioni sono migliorate quando viene eseguita in modalità esclusiva.|Per impostare questa opzione in modo dinamico, usare la parola chiave **Exclusive** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Timeout pagina|Specifica il periodo di tempo, in decimi di secondo, che una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Il valore predefinito è 600 decimi di secondo (60 secondi). Questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> Il timeout della pagina non può essere 0 a causa di un ritardo intrinseco. Il timeout della pagina non può essere inferiore al ritardo intrinseco, anche se l'opzione Timeout pagina è impostata al di sotto di tale valore.|Per impostare questa opzione in modo dinamico, usare la parola chiave **PAGETIMEOUT** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Sola lettura|Designa il database come di sola lettura.|Per impostare questa opzione in modo dinamico, usare la parola chiave **ReadOnly** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Seleziona directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory che contiene i file a cui si vuole accedere.<br /><br /> Quando si definisce una directory di origine dati, specificare la directory in cui si trovano i file usati più di frequente. Il driver ODBC utilizza questa directory come directory predefinita. Copiare altri file in questa directory se vengono usati di frequente. In alternativa, è possibile qualificare i nomi di file in un'istruzione SELECT con il nome della directory:<br /><br /> Seleziona \* da C:\MYDIR\EMP<br /><br /> In alternativa, è possibile specificare una nuova directory predefinita usando la funzione **SQLSetConnectOption** con l'opzione SQL_CURRENT_QUALIFIER.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Mostra righe eliminate|Specifica se è possibile recuperare o posizionare le righe contrassegnate come eliminate. Se deselezionata, le righe eliminate non vengono visualizzate. Se questa opzione è selezionata, le righe eliminate vengono gestite come righe non eliminate. Per impostazione predefinita, l'opzione è deselezionata.|Per impostare questa opzione in modo dinamico, usare la parola chiave **Deleted** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|
