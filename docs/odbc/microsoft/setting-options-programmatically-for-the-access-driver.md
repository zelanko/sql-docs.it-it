---
title: Impostazione delle opzioni a livello di codice per il driver di accesso Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a90f0a20569a2a0a5bb93dec7aa4b95b50093dc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300791"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Impostazione delle opzioni a livello di codice per il driver Access

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Dimensione buffer|Dimensione del buffer interno, in kilobyte, utilizzata da Microsoft Access per trasferire dati da e verso il disco. La dimensione predefinita del buffer è 2048 KB (visualizzato come 2048). È possibile immettere qualsiasi valore intero divisibile per 256.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave MAXBUFFERSI-E in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Data Source Name|Nome che identifica l'origine dati, ad esempio Retribuzioni o Personale.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DSN** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Database|È possibile impostare un'origine dati di Microsoft Access senza selezionare o creare un database. Se al momento dell'installazione non viene fornito alcun database, all'utente verrà richiesto di scegliere un file di database per la connessione all'origine dati.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DBQ** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Descrizione|Descrizione facoltativa dei dati nell'origine dati. ad esempio, "Data di assunzione, cronologia degli stipendi e revisione corrente di tutti i dipendenti".|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DESCRIPTION** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Esclusivo|Se la casella **Esclusivo** è selezionata, il database verrà aperto in modalità Esclusiva ed è accessibile da un solo utente alla volta. Le prestazioni sono migliorate durante l'esecuzione in modalità esclusiva.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **EXCLUSIVE** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|ImplicitCommitSync|Determina il modo in cui le modifiche apportate all'esterno di una transazione vengono scritte nel database. Questo valore è inizialmente impostato su "Sì", il che significa che il driver di Microsoft Access attenderà il completamento dei commit in una transazione interna/implicita.|Questa opzione è inclusa nella finestra di dialogo **Imposta opzioni avanzate** per il driver di Microsoft Access.|  
|Timeout pagina|Specifica il periodo di tempo, in millisecondi, durante il quale una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Per il driver di Microsoft Access, il valore predefinito è 500 millisecondi (0,5 secondi). Questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> Il timeout della pagina non può essere 0 a causa di un ritardo intrinseco. Il timeout della pagina non può essere inferiore al ritardo intrinseco, anche se l'opzione di timeout della pagina è impostata al di sotto di tale valore.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **PAGETIMEOUT** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Sola lettura|Designa il database come di sola lettura.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **READONLY** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Database di sistema|Il percorso completo del database di sistema di Microsoft Access da utilizzare con il database di Microsoft Access a cui si desidera accedere.<br /><br /> Fare clic sul pulsante **Database di** sistema per selezionare il database di sistema da utilizzare. Il driver ODBC di Microsoft Access richiede all'utente un nome e una password. Il nome predefinito è Admin e la password predefinita in Microsoft Access per l'utente Admin è una stringa vuota.<br /><br /> Per aumentare la sicurezza del database di Microsoft Access, creare un nuovo utente per sostituire l'utente Admin ed eliminare l'utente Admin oppure modificare gli oggetti a cui l'utente Admin ha accesso.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **SYSTEMDB** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Threads|Numero di thread in background per il motore da utilizzare. Per il driver di Microsoft Access, il valore predefinito è 3, ma può essere modificato. L'utente potrebbe voler aumentare il numero di thread se è presente una grande quantità di attività nel database.<br /><br /> Questa opzione è inclusa nella finestra di dialogo **Imposta opzioni avanzate** per il driver di Microsoft Access.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **THREADS** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|UserCommitSync (Sincronizzazione utente)|Determina se il driver di Microsoft Access eseguirà una transazione esplicita definita dall'utente in modo asincrono. Questo valore è inizialmente impostato su "Sì", il che significa che il driver di Microsoft Access attenderà il completamento dei commit in una transazione definita dall'utente.<br /><br /> L'impostazione di questa opzione su False può avere conseguenze imprevedibili in un ambiente multiutente.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **USERCOMMITSYNC** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|
