---
title: Impostazione delle opzioni a livello di codice per il driver Excel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 47181fca07aff7b2a0d418b8852cfce47cf9e501
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063518"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Impostazione delle opzioni a livello di codice per il driver Excel

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Data Source Name|Nome che identifica l'origine dati, ad esempio Payroll o personale.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DSN** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Database|Un'origine dati di Microsoft Access può essere configurata senza selezionare o creare un database. Se non viene fornito alcun database durante l'installazione, all'utente verrà richiesto di scegliere un file di database durante la connessione all'origine dati.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DBQ** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Descrizione|Descrizione facoltativa dei dati nell'origine dati. ad esempio, "Data assunzione, cronologia stipendio e revisione corrente di tutti i dipendenti".|Per impostare questa opzione in modo dinamico, usare la parola chiave **Description** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Directory|Consente di visualizzare la directory attualmente selezionata.<br /><br /> Per i file di Microsoft Excel 3.0/4.0, la visualizzazione del percorso è denominata "directory", mentre per i file di Microsoft Excel 5,0, 7,0 o 97 la visualizzazione del percorso è denominata "cartella di lavoro".|Per impostare questa opzione in modo dinamico, usare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Sola lettura|Designa il database come di sola lettura.|Per impostare questa opzione in modo dinamico, usare la parola chiave **ReadOnly** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Righe da analizzare|Numero di righe da analizzare per determinare il tipo di dati di ogni colonna. Il tipo di dati viene determinato in base al numero massimo di tipi di dati trovati. Se vengono rilevati dati che non corrispondono al tipo di dati ipotizzato per la colonna, il tipo di dati verrà restituito come valore NULL.<br /><br /> Per il driver Microsoft Excel, è possibile immettere un numero compreso tra 1 e 16 per le righe da analizzare. Il valore predefinito è 8. Se è impostato su 0, viene eseguita l'analisi di tutte le righe. (Un numero al di fuori del limite restituirà un errore).|Per impostare questa opzione in modo dinamico, usare la parola chiave **MaxScanRows** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Seleziona directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory contenente i file a cui si vuole accedere.<br /><br /> Quando si definisce una directory di origine dati (per tutti i driver ad eccezione di Microsoft Access), specificare la directory in cui si trovano i file usati più di frequente. Il driver ODBC utilizza questa directory come directory predefinita. Copiare altri file in questa directory se vengono usati di frequente. In alternativa, è possibile qualificare i nomi di file in un'istruzione SELECT con il nome della directory:<br /><br /> Seleziona \* da C:\MYDIR\EMP<br /><br /> In alternativa, è possibile specificare una nuova directory predefinita usando la funzione **SQLSetConnectOption** con l'opzione SQL_CURRENT_QUALIFIER.<br /><br /> Per i file di Microsoft Excel 3,0 o 4,0, la visualizzazione del percorso è denominata "directory" e il pulsante di selezione del percorso è denominato "Seleziona directory". Per i file di Microsoft Excel 5,0, 7,0 o 97, la visualizzazione del percorso è denominata "cartella di lavoro" e il pulsante di selezione del percorso è denominato "Seleziona cartella di lavoro". Quando si definisce una directory di origine dati, specificare la directory in cui si trovano i file di Microsoft Excel utilizzati più di frequente per Microsoft Excel 3.0/4.0 o la directory in cui si trova il file della cartella di lavoro per Microsoft Excel 5,0, 7,0 o 97. **Utilizzare la directory corrente** è disabilitato per Microsoft Excel 5,0, 7,0 e 97.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|
