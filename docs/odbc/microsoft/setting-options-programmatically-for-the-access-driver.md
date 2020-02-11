---
title: Impostazione delle opzioni a livello di codice per il driver di accesso | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 688716e9b7ba89500a4d2e8a579da42972e43d0c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063550"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Impostazione delle opzioni a livello di codice per il driver Access

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Dimensioni del buffer|Dimensioni del buffer interno, in kilobyte, utilizzate da Microsoft Access per trasferire dati da e verso il disco. Le dimensioni predefinite del buffer sono 2048 KB (visualizzate come 2048). È possibile immettere qualsiasi valore intero divisibile per 256.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave MAXBUFFERSIZE in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Data Source Name|Nome che identifica l'origine dati, ad esempio Payroll o personale.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DSN** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Database|Un'origine dati di Microsoft Access può essere configurata senza selezionare o creare un database. Se non viene fornito alcun database durante l'installazione, all'utente verrà richiesto di scegliere un file di database durante la connessione all'origine dati.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DBQ** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Descrizione|Descrizione facoltativa dei dati nell'origine dati. ad esempio, "Data assunzione, cronologia stipendio e revisione corrente di tutti i dipendenti".|Per impostare questa opzione in modo dinamico, usare la parola chiave **Description** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Esclusivo|Se si seleziona la casella **esclusiva** , il database verrà aperto in modalità esclusiva ed è possibile accedervi da un solo utente alla volta. Le prestazioni sono migliorate durante l'esecuzione in modalità esclusiva.|Per impostare questa opzione in modo dinamico, usare la parola chiave **Exclusive** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|ImplicitCommitSync|Determina il modo in cui le modifiche apportate all'esterno di una transazione vengono scritte nel database. Questo valore inizialmente è impostato su "Sì", il che significa che il driver Microsoft Access attenderà il completamento dei commit in una transazione interna/implicita.|Questa opzione è inclusa nella finestra di dialogo **Imposta opzioni avanzate** per il driver Microsoft Access.|  
|Timeout pagina|Specifica il periodo di tempo, in millisecondi, durante il quale una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Per il driver Microsoft Access, il valore predefinito è 500 millisecondi (0,5 secondi). Questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> Il timeout della pagina non può essere 0 a causa di un ritardo intrinseco. Il timeout della pagina non può essere inferiore al ritardo intrinseco, anche se l'opzione Timeout pagina è impostata al di sotto di tale valore.|Per impostare questa opzione in modo dinamico, usare la parola chiave **PAGETIMEOUT** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Sola lettura|Designa il database come di sola lettura.|Per impostare questa opzione in modo dinamico, usare la parola chiave **ReadOnly** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Database di sistema|Percorso completo del database di sistema Microsoft Access da usare con il database di Microsoft Access a cui si vuole accedere.<br /><br /> Fare clic sul pulsante **database di sistema** per selezionare il database di sistema da utilizzare. Il driver ODBC Microsoft Access richiede un nome e una password per l'utente. Il nome predefinito è admin e la password predefinita in Microsoft Access per l'utente amministratore è una stringa vuota.<br /><br /> Per aumentare la sicurezza del database di Microsoft Access, creare un nuovo utente per sostituire l'utente amministratore ed eliminare l'utente amministratore oppure modificare gli oggetti a cui l'utente amministratore ha accesso.|Per impostare questa opzione in modo dinamico, usare la parola chiave **SYSTEMDB** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Threads|Numero di thread in background per il motore da usare. Per il driver Microsoft Access, il valore predefinito è 3, ma è possibile modificarlo. Se nel database è presente una grande quantità di attività, è possibile che l'utente desideri aumentare il numero di thread.<br /><br /> Questa opzione è inclusa nella finestra di dialogo **Imposta opzioni avanzate** per il driver Microsoft Access.|Per impostare questa opzione in modo dinamico, usare la parola chiave **Threads** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|UserCommitSync|Determina se il driver Microsoft Access eseguirà in modo asincrono una transazione esplicita definita dall'utente. Questo valore inizialmente è impostato su "Sì", il che significa che il driver Microsoft Access attenderà il completamento dei commit in una transazione definita dall'utente.<br /><br /> L'impostazione di questa opzione su false può comportare conseguenze imprevedibili in un ambiente multiutente.|Per impostare questa opzione in modo dinamico, usare la parola chiave **USERCOMMITSYNC** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|
