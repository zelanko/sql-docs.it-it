---
title: Impostazione delle opzioni a livello di codice per il Driver Access | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063550"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Impostazione delle opzioni a livello di codice per il driver Access

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Dimensioni del buffer|Le dimensioni del buffer interno, espressa in kilobyte, che viene utilizzata da Microsoft Access per trasferire i dati da e verso il disco. Le dimensioni del buffer predefinita sono 2048 KB (visualizzato come 2048). Possono essere immessi numeri interi divisibili per 256.|Per impostare questa opzione in modo dinamico, usare la parola chiave MAXBUFFERSIZE in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Nome origine dati|Un nome che identifica l'origine dati, ad esempio Payroll o personale.|Per impostare questa opzione in modo dinamico, usare il **DSN** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Database|Un'origine dati Microsoft Access da impostare senza selezionare o creare un database. Se viene specificato alcun database al momento dell'installazione, l'utente verrà chiesto di scegliere un file di database durante la connessione all'origine dati.|Per impostare questa opzione in modo dinamico, usare il **DBQ** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Descrizione|Una descrizione facoltativa dei dati nell'origine dati; ad esempio, "Hire data, cronologia degli stipendi e situazione corrente di tutti i dipendenti."|Per impostare questa opzione in modo dinamico, usare il **DESCRIPTION** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Exclusive|Se il **esclusivo** casella è selezionata, il database verrà aperto in modalità esclusiva e sono accessibili da un solo utente alla volta. Le prestazioni sono ottimizzate durante l'esecuzione in modalità esclusiva.|Per impostare questa opzione in modo dinamico, usare il **esclusivo** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|ImplicitCommitSync|Determina come le modifiche apportate all'esterno di una transazione vengono scritti nel database. Questo valore è inizialmente impostato su "Sì", il che significa che il driver Microsoft Access rimarrà in attesa per i commit in una transazione interna/implicita per essere completati.|Questa opzione è inclusa nel **Imposta opzioni avanzate** finestra di dialogo per il driver Microsoft Access.|  
|Timeout di pagina|Specifica il periodo di tempo, espresso in millisecondi, che una pagina, se non utilizzato, rimane nel buffer prima della rimozione. Per il driver Microsoft Access, il valore predefinito è 500 millisecondi (0,5 secondi). Questa opzione si applica a tutte le origini dati che usano il driver ODBC.<br /><br /> Il timeout della pagina non può essere 0 a causa di un ritardo inerente. Il timeout della pagina non può essere minore del ritardo inerente, anche se è impostata l'opzione di timeout della pagina di sotto di tale valore.|Per impostare questa opzione in modo dinamico, usare il **PAGETIMEOUT** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Sola lettura|Definisce il database in sola lettura.|Per impostare questa opzione in modo dinamico, usare il **READONLY** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Database di sistema|Il percorso completo del database di sistema di Microsoft Access da utilizzare con il database Microsoft Access che si desidera accedere.<br /><br /> Scegliere il **Database di sistema** pulsante per selezionare il database di sistema da utilizzare. Il driver ODBC Microsoft Access richiede all'utente un nome e una password. Il nome predefinito è Admin e la password predefinita in Microsoft Access per l'utente amministratore è una stringa vuota.<br /><br /> Per aumentare la sicurezza del database Microsoft Access, creare un nuovo utente per l'utente amministratore di sostituire ed eliminare l'utente amministratore o modificare gli oggetti a cui l'utente amministratore ha accesso.|Per impostare questa opzione in modo dinamico, usare il **SYSTEMDB** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Thread|Il numero di thread in background per il motore da usare. Per il driver Microsoft Access, questo valore predefinito è 3, ma può essere modificato. L'utente potrebbe voler aumentare il numero di thread se è presente una grande quantità di attività nel database.<br /><br /> Questa opzione è inclusa nel **Imposta opzioni avanzate** finestra di dialogo per il driver Microsoft Access.|Per impostare questa opzione in modo dinamico, usare il **thread** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|UserCommitSync|Determina se il driver Microsoft Access verrà eseguite in modo asincrono un transazioni esplicite definite dall'utente. Questo valore è inizialmente impostato su "Sì", il che significa che il driver Microsoft Access rimarrà in attesa per i commit in una transazione definita dall'utente per il completamento.<br /><br /> Impostando questa opzione su False può avere conseguenze imprevedibili in un ambiente multiutente.|Per impostare questa opzione in modo dinamico, usare il **USERCOMMITSYNC** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|
