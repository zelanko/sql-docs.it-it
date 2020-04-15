---
title: SQLConfigDataSource (Driver file di testo) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d2809f9b15dd6843e4404c7cf1887c3caa015a3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283921"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (driver file di testo)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di file di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La funzione **SQLConfigDataSource** utilizzata per aggiungere, modificare o eliminare un'origine dati in modo dinamico utilizza le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|SET DI CARATTERI|Per il driver di testo, OEM o ANSI.|  
|COLNAMEHEADER|Per il driver di testo, indica se il primo record di dati specificherà i nomi delle colonne. VERO o FALSO.|  
|DEFAULTDIR (DISE)|Specifica del percorso della directory.|  
|DESCRIZIONE|Descrizione dei dati nell'origine dati.<br /><br /> In questo modo viene impostata la stessa opzione **Descrizione** nella finestra di dialogo di installazione.|  
|DRIVER|Specifica del percorso della DLL del driver.|  
|DRIVERID|Un ID intero per il driver. 27 (Testo)|  
|Estensioni|Elenca le estensioni di file dei file di testo nell'origine dati.<br /><br /> In questo modo viene impostata la stessa opzione di **Elenco estensioni** nella finestra di dialogo di installazione.|  
|Fil|Tipo di file Testo|  
|Filetype|Tipo di file per il driver di testo (testo).|  
|FORMAT|Per il driver di testo, può essere FIXEDLENGTH, TABDELIMITED, CSVDELIMITED (da una virgola) o DELIMITED() (dal carattere speciale specificato tra parentesi). Il carattere speciale è di un carattere in lunghezza e può essere in formato carattere, decimale o esadecimale.|  
|NUMERO MAXSCANROWS|Numero di righe da analizzare quando si imposta il tipo di dati di una colonna in base ai dati esistenti.<br /><br /> Per il driver di testo, è possibile immettere un numero compreso tra 1 e 32767 per il numero di righe da scansionare; tuttavia, il valore predefinito sarà sempre 25. (Un numero al di fuori del limite restituirà un errore.)<br /><br /> In questo modo viene impostata la stessa opzione **Righe da eseguire la scansione** nella finestra di dialogo di configurazione.|  
|READONLY|TRUE per rendere il file di sola lettura; FALSE per rendere il file non di sola lettura.<br /><br /> In questo modo viene impostata la stessa opzione **Sola lettura** nella finestra di dialogo di installazione.|
