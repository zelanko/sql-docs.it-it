---
title: Impostazione delle opzioni a livello di codice per il Driver per Excel | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063518"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Impostazione delle opzioni a livello di codice per il driver Excel

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Nome origine dati|Un nome che identifica l'origine dati, ad esempio Payroll o personale.|Per impostare questa opzione in modo dinamico, usare il **DSN** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Database|Un'origine dati Microsoft Access da impostare senza selezionare o creare un database. Se viene specificato alcun database al momento dell'installazione, l'utente verrà chiesto di scegliere un file di database durante la connessione all'origine dati.|Per impostare questa opzione in modo dinamico, usare il **DBQ** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Descrizione|Una descrizione facoltativa dei dati nell'origine dati; ad esempio, "Hire data, cronologia degli stipendi e situazione corrente di tutti i dipendenti."|Per impostare questa opzione in modo dinamico, usare il **DESCRIPTION** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Directory|Consente di visualizzare la directory attualmente selezionata.<br /><br /> Per i file di Microsoft Excel versione 3.0 o 4.0, la visualizzazione del percorso con l'etichetta "Directory", mentre per Microsoft Excel 5.0, 7.0, 97 o file, la visualizzazione del percorso con l'etichetta "Cartella di lavoro".|Per impostare questa opzione in modo dinamico, usare il **DEFAULTDIR** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Sola lettura|Definisce il database in sola lettura.|Per impostare questa opzione in modo dinamico, usare il **READONLY** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Righe da analizzare|Il numero di righe da esaminare per determinare il tipo di dati di ogni colonna. Il tipo di dati viene determinato dato il numero massimo di tipi di dati disponibili. Se vengono rilevati dati che non corrisponde al tipo di dati previsto per la colonna, il tipo di dati restituirà come valore NULL.<br /><br /> Per il driver di Microsoft Excel, è possibile immettere un numero da 1 a 16 per le righe da analizzare. Il valore predefinito è 8, mentre Se è impostato su 0, vengono analizzate tutte le righe. (Un numero di fuori del limite verrà restituito un errore).|Per impostare questa opzione in modo dinamico, usare il **MAXSCANROWS** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Selezionare la Directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory che contiene i file che si desidera accedere.<br /><br /> Quando si definisce una directory di origine dati (per tutti i driver, ad eccezione di Microsoft Access), specificare la directory in cui si trovano i file più comunemente utilizzati. Il driver ODBC usa tale directory come directory predefinita. Copiare altri file in questa directory, se vengono usati frequentemente. In alternativa, è possibile qualificare nomi di file in un'istruzione SELECT con il nome della directory:<br /><br /> SELEZIONARE \* DA C:\MYDIR\EMP<br /><br /> Oppure, è possibile specificare una nuova directory predefinita usando il **SQLSetConnectOption** canonica con l'opzione SQL_CURRENT_QUALIFIER.<br /><br /> Per Microsoft Excel 3.0 o 4.0 file, la visualizzazione del percorso è denominata "Directory" e pulsante di selezione del percorso con l'etichetta "Seleziona Directory". Per i file di Microsoft Excel 97, versione 7.0 o 5.0, la visualizzazione del percorso è denominata "Cartella di lavoro" e pulsante di selezione del percorso con l'etichetta "Selezione cartella di lavoro". Quando si definisce una directory di origine dati, specificare la directory in cui i file Microsoft Excel più comunemente utilizzati si trovano per Microsoft Excel versione 3.0 o 4.0 o la directory in cui il file della cartella di lavoro si trova per Microsoft Excel 97, versione 7.0 o 5.0. **Usare la Directory corrente** è disabilitata per Microsoft Excel 97, 7.0 e 5.0.|Per impostare questa opzione in modo dinamico, usare il **DEFAULTDIR** parola chiave in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|
