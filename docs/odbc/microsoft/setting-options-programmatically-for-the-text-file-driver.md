---
title: Impostazione delle opzioni a livello di codice per il driver del file di testo | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300751"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>Impostazione delle opzioni a livello di codice per il driver file di testo

|Opzione|Descrizione|Metodo|  
|------------|-----------------|------------|  
|Data Source Name|Nome che identifica l'origine dati, ad esempio Payroll o personale.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DSN** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Definisci formato|Consente di visualizzare la finestra di dialogo **Definisci formato testo** e consente di specificare lo schema per le singole tabelle della directory dell'origine dati.|Questa opzione non può essere impostata in modo dinamico tramite una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Descrizione|Descrizione facoltativa dei dati nell'origine dati. ad esempio, "Data assunzione, cronologia stipendio e revisione corrente di tutti i dipendenti".|Per impostare questa opzione in modo dinamico, usare la parola chiave **Description** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Directory|Consente di selezionare la directory di destinazione.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Elenco estensioni|Elenca le estensioni dei nomi di file di testo nell'origine dati. Quando si utilizza il driver di testo, viene creato un file senza estensione quando l'istruzione CREATE TABLE viene eseguita con un nome privo di estensione. Altri driver creano un file con estensione predefinita quando non viene fornita alcuna estensione. Per creare un file con estensione txt, è necessario includere l'estensione nel nome. Per visualizzare i file senza estensioni nella finestra di dialogo **Definisci formato testo** , "*." deve essere aggiunto all'elenco delle estensioni.|Per impostare questa opzione in modo dinamico, usare la parola chiave **Extensions** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Sola lettura|Designa il database come di sola lettura.|Per impostare questa opzione in modo dinamico, usare la parola chiave **ReadOnly** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Righe da analizzare|Numero di righe da analizzare per determinare il tipo di dati di ogni colonna. Il tipo di dati viene determinato in base al numero massimo di tipi di dati trovati. Se vengono rilevati dati che non corrispondono al tipo di dati ipotizzato per la colonna, il tipo di dati verrà restituito come valore NULL.<br /><br /> Per il driver di testo, è possibile immettere un numero compreso tra 1 e 32767 per il numero di righe da analizzare. Tuttavia, il valore predefinito è sempre 25. (Un numero al di fuori del limite restituirà un errore).|Per impostare questa opzione in modo dinamico, usare la parola chiave **MaxScanRows** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Seleziona directory|Visualizza una finestra di dialogo in cui è possibile selezionare una directory contenente i file a cui si vuole accedere.<br /><br /> Quando si definisce una directory di origine dati, specificare la directory in cui si trovano i file usati più di frequente. Il driver ODBC utilizza questa directory come directory predefinita. Copiare altri file in questa directory se vengono usati di frequente. In alternativa, è possibile qualificare i nomi di file in un'istruzione SELECT con il nome della directory:`SELECT * FROM C:\MYDIR\EMP`<br /><br /> In alternativa, è possibile specificare una nuova directory predefinita usando la funzione **SQLSetConnectOption** con l'opzione SQL_CURRENT_QUALIFIER.|Per impostare questa opzione in modo dinamico, usare la parola chiave **DEFAULTDIR** in una chiamata a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|
