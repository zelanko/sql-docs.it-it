---
title: Impostazione delle opzioni a livello di codice per il driver di Excel Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fcd5542e4beee1f7c7a30d5e0ee9f2815a3f0b6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300771"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Impostazione delle opzioni a livello di codice per il driver Excel

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Data Source Name|Nome che identifica l'origine dati, ad esempio Retribuzioni o Personale.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DSN** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Database|È possibile impostare un'origine dati di Microsoft Access senza selezionare o creare un database. Se al momento dell'installazione non viene fornito alcun database, all'utente verrà richiesto di scegliere un file di database per la connessione all'origine dati.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DBQ** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Descrizione|Descrizione facoltativa dei dati nell'origine dati. ad esempio, "Data di assunzione, cronologia degli stipendi e revisione corrente di tutti i dipendenti".|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DESCRIPTION** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Directory|Visualizza la directory attualmente selezionata.<br /><br /> Per i file di Microsoft Excel 3.0/4.0, la visualizzazione del percorso è denominata "Directory", mentre per i file di Microsoft Excel 5.0, 7.0 o 97, la visualizzazione del percorso è denominata "Cartella di lavoro".|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Sola lettura|Designa il database come di sola lettura.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **READONLY** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Righe da scansionare|Numero di righe da scansionare per determinare il tipo di dati di ogni colonna. Il tipo di dati viene determinato in base al numero massimo di tipi di dati trovati. Se vengono rilevati dati che non corrispondono al tipo di dati rilevato per la colonna, il tipo di dati verrà restituito come valore NULL.<br /><br /> Per il driver Microsoft Excel, è possibile immettere un numero compreso tra 1 e 16 per le righe da eseguire la scansione. Il valore predefinito è 8; se è impostato su 0, vengono analizzate tutte le righe. (Un numero al di fuori del limite restituirà un errore.)|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **MAXSCANROWS** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Seleziona directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory contenente i file a cui si desidera accedere.<br /><br /> Quando si definisce una directory dell'origine dati (per tutti i driver ad eccezione di Microsoft Access), specificare la directory in cui si trovano i file utilizzati più di più di seguito. Il driver ODBC utilizza questa directory come directory predefinita. Copiare altri file in questa directory se vengono utilizzati di frequente. In alternativa, è possibile qualificare i nomi di file in un'istruzione SELECT con il nome della directory:<br /><br /> SELECT \* FROM:<br /><br /> In alternativa, è possibile specificare una nuova directory predefinita utilizzando la funzione **SQLSetConnectOption** con l'opzione SQL_CURRENT_QUALIFIER.<br /><br /> Per i file di Microsoft Excel 3.0 o 4.0, la visualizzazione del percorso è denominata "Directory" e il pulsante di selezione del percorso è etichettato "Seleziona directory". Per i file di Microsoft Excel 5.0, 7.0 o 97, la visualizzazione del percorso è denominata "Cartella di lavoro" e il pulsante di selezione del percorso è etichettato "Seleziona cartella di lavoro". Quando si definisce una directory dell'origine dati, specificare la directory in cui si trovano i file di Microsoft Excel più comunemente utilizzati per Microsoft Excel 3.0/4.0 o la directory in cui si trova il file della cartella di lavoro per Microsoft Excel 5.0, 7.0 o 97. **Usa directory corrente** è disabilitato per Microsoft Excel 5.0, 7.0 e 97.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|
