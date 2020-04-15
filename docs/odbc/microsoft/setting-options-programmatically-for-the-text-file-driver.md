---
title: Impostazione delle opzioni a livello di codice per il driver di file di testo Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e19c3b49479047bc92a7b6f72359d4951d8df16e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300751"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>Impostazione delle opzioni a livello di codice per il driver file di testo

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Data Source Name|Nome che identifica l'origine dati, ad esempio Retribuzioni o Personale.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DSN** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Definisci formato|Visualizza la finestra di dialogo **Definisci formato testo** e consente di specificare lo schema per le singole tabelle nella directory dell'origine dati.|Questa opzione non può essere impostata in modo dinamico da una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Descrizione|Descrizione facoltativa dei dati nell'origine dati. ad esempio, "Data di assunzione, cronologia degli stipendi e revisione corrente di tutti i dipendenti".|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DESCRIPTION** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Directory|Seleziona la directory di destinazione.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Elenco estensioni|Elenca le estensioni di file dei file di testo nell'origine dati. Quando viene utilizzato il driver di testo, viene creato un file senza estensione quando viene eseguita l'istruzione CREATE TABLE con un nome senza estensione. Altri driver creano un file con un'estensione predefinita quando non viene fornita alcuna estensione. Per creare un file con estensione txt, l'estensione deve essere inclusa nel nome. Per visualizzare i file senza estensioni nella finestra di dialogo **Definisci formato** testo, ovvero ""." deve essere aggiunto all'elenco delle estensioni.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **EXTENSIONS** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Sola lettura|Designa il database come di sola lettura.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **READONLY** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Righe da scansionare|Numero di righe da scansionare per determinare il tipo di dati di ogni colonna. Il tipo di dati viene determinato in base al numero massimo di tipi di dati trovati. Se vengono rilevati dati che non corrispondono al tipo di dati rilevato per la colonna, il tipo di dati verrà restituito come valore NULL.<br /><br /> Per il driver di testo, è possibile immettere un numero compreso tra 1 e 32767 per il numero di righe da scansionare; tuttavia, il valore predefinito sarà sempre 25. (Un numero al di fuori del limite restituirà un errore.)|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **MAXSCANROWS** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Seleziona directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory contenente i file a cui si desidera accedere.<br /><br /> Quando si definisce una directory dell'origine dati, specificare la directory in cui si trovano i file utilizzati più di più di seguito. Il driver ODBC utilizza questa directory come directory predefinita. Copiare altri file in questa directory se vengono utilizzati di frequente. In alternativa, è possibile qualificare i nomi di file in un'istruzione SELECT con il nome della directory:`SELECT * FROM C:\MYDIR\EMP`<br /><br /> In alternativa, è possibile specificare una nuova directory predefinita utilizzando la funzione **SQLSetConnectOption** con l'opzione SQL_CURRENT_QUALIFIER.|Per impostare questa opzione in modo dinamico, utilizzare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|
