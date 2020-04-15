---
title: SQLConfigDataSource (driver di Excel) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a76482acd1182d900336d7ac9826b16968e00caa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293011"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (driver Excel)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di Excel.This topic provides Excel Driver-specific information. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La funzione **SQLConfigDataSource** utilizzata per aggiungere, modificare o eliminare un'origine dati in modo dinamico utilizza le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|DBQ|Per il driver di Microsoft Excel quando si accede a file di Microsoft Excel 5.0 o versioni successive, il nome del file della cartella di lavoro.<br /><br /> In questo modo viene impostata la stessa opzione **Di Database** nella finestra di dialogo di installazione.|  
|DEFAULTDIR (DISE)|Specifica del percorso della directory.<br /><br /> In questo modo viene impostata la stessa opzione **di Seleziona directory** o Seleziona cartella di **lavoro** nella finestra di dialogo di installazione.|  
|DESCRIZIONE|Descrizione dei dati nell'origine dati.<br /><br /> In questo modo viene impostata la stessa opzione **Descrizione** nella finestra di dialogo di installazione.|  
|DRIVER|Specifica del percorso della DLL del driver.|  
|DRIVERID|Un ID intero per il driver.<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|Fil|Tipo di file, ad esempio Excel 3.0, Excel 4.0, Excel 5.0, Excel 7.0, Excel 97, Excel 2000 o Excel 2003.|  
|FIRSTROWHASNAMES|Indica se le celle della prima riga dell'intervallo contengono i nomi di colonna per la tabella (1) o meno (0).|  
|NUMERO MAXSCANROWS|Numero di righe da analizzare quando si imposta il tipo di dati di una colonna in base ai dati esistenti.<br /><br /> È possibile immettere un numero compreso tra 1 e 16 per le righe da scansionare. Il valore predefinito è 8; se è impostato su 0, vengono analizzate tutte le righe. (Un numero al di fuori del limite restituirà un errore.)<br /><br /> In questo modo viene impostata la stessa opzione **Righe da eseguire la scansione** nella finestra di dialogo di configurazione.|  
|READONLY|TRUE per rendere il file di sola lettura; FALSE per rendere il file non di sola lettura.<br /><br /> In questo modo viene impostata la stessa opzione **Sola lettura** nella finestra di dialogo di installazione.|  
|Discussioni|Numero di thread in background per il motore da utilizzare. Per il driver di Microsoft Access, il valore predefinito è 3, ma può essere modificato. Per dBASE, MicrosoftExceldriver questo valore è 3 e non può essere modificato.<br /><br /> In questo modo viene impostata la stessa opzione **di Thread** nella finestra di dialogo di installazione.|
