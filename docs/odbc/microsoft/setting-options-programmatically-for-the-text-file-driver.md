---
title: Impostazione delle opzioni a livello di codice per il Driver del File di testo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e1a28e5c7ccf3c701e5f97440cd97ed843ab53dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063501"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>Impostazione delle opzioni a livello di codice per il driver file di testo

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Nome origine dati|Un nome che identifica l'origine dati, ad esempio Payroll o personale.|Per impostare questa opzione in modo dinamico, usare il **DSN** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Definire il formato|Consente di visualizzare il **Definisci formato testo** nella finestra di dialogo e consente di specificare lo schema per le singole tabelle nella directory di origine dati.|Questa opzione non può essere impostata in modo dinamico mediante una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Descrizione|Una descrizione facoltativa dei dati nell'origine dati; ad esempio, "Hire data, cronologia degli stipendi e situazione corrente di tutti i dipendenti."|Per impostare questa opzione in modo dinamico, usare il **DESCRIPTION** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Directory|Seleziona directory di destinazione.|Per impostare questa opzione in modo dinamico, usare il **DEFAULTDIR** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Elenco di estensioni|Elenca le estensioni dei file di testo sull'origine dati. Quando viene usato il driver di testo, viene creato un file senza estensione quando viene eseguita l'istruzione CREATE TABLE con un nome che non dispone di estensione. Altri driver di creare un file con estensione predefinita quando non viene specificato estensione. Per creare un file con estensione txt, l'estensione deve essere incluso nel nome. Per visualizzare i file senza estensione nel **Definisci formato testo** nella finestra di dialogo "*." deve essere aggiunto all'elenco di estensioni.|Per impostare questa opzione in modo dinamico, usare il **EXTENSIONS** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Sola lettura|Definisce il database in sola lettura.|Per impostare questa opzione in modo dinamico, usare il **READONLY** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Righe da analizzare|Il numero di righe da esaminare per determinare il tipo di dati di ogni colonna. Il tipo di dati viene determinato dato il numero massimo di tipi di dati disponibili. Se vengono rilevati dati che non corrisponde al tipo di dati previsto per la colonna, il tipo di dati restituirà come valore NULL.<br /><br /> Per il driver di testo, è possibile immettere un numero compreso tra 1 e 32767 per il numero di righe da analizzare; Tuttavia, il valore verrà sempre aperta a 25. (Un numero di fuori del limite verrà restituito un errore).|Per impostare questa opzione in modo dinamico, usare il **MAXSCANROWS** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Selezionare la Directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory che contiene i file che si desidera accedere.<br /><br /> Quando la definizione di una directory di origine dati specifica la directory in cui la più comunemente usati i file si trovano. Il driver ODBC usa tale directory come directory predefinita. Copiare altri file in questa directory, se vengono usati frequentemente. In alternativa, è possibile qualificare nomi di file in un'istruzione SELECT con il nome della directory: `SELECT * FROM C:\MYDIR\EMP`<br /><br /> Oppure, è possibile specificare una nuova directory predefinita usando il **SQLSetConnectOption** canonica con l'opzione SQL_CURRENT_QUALIFIER.|Per impostare questa opzione in modo dinamico, usare il **DEFAULTDIR** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|
