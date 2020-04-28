---
title: ODBC Jet SQLConfigDataSource (driver Excel) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81293011"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (driver Excel)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di Excel. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La funzione **SQLConfigDataSource** utilizzata per aggiungere, modificare o eliminare un'origine dati in modo dinamico utilizza le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|DBQ|Per il driver Microsoft Excel per l'accesso a file di Microsoft Excel 5,0 o versioni successive, il nome del file della cartella di lavoro.<br /><br /> In questo modo viene impostata la stessa opzione del **database** nella finestra di dialogo di installazione.|  
|DEFAULTDIR|Specifica del percorso della directory.<br /><br /> Verrà impostata la stessa opzione **Seleziona directory** o **Seleziona cartella di lavoro** nella finestra di dialogo Imposta.|  
|DESCRIZIONE|Descrizione dei dati nell'origine dati.<br /><br /> Questa opzione consente di impostare la stessa opzione della **Descrizione** nella finestra di dialogo di installazione.|  
|DRIVER|Specifica del percorso per la DLL del driver.|  
|DRIVERID|ID di tipo integer per il driver.<br /><br /> 534 (Microsoft Excel 3,0)<br /><br /> 278 (Microsoft Excel 4,0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|Tipo di file, ad esempio Excel 3,0, Excel 4,0, Excel 5,0, Excel 7,0, Excel 97, Excel 2000 o Excel 2003.|  
|FIRSTROWHASNAMES|Indica se le celle della prima riga dell'intervallo contengono i nomi di colonna per la tabella (1) o meno (0).|  
|MAXSCANROWS|Numero di righe da analizzare quando si imposta il tipo di dati di una colonna in base ai dati esistenti.<br /><br /> Per le righe da analizzare è possibile immettere un numero compreso tra 1 e 16. Il valore predefinito è 8. Se è impostato su 0, viene eseguita l'analisi di tutte le righe. (Un numero al di fuori del limite restituirà un errore).<br /><br /> Consente di impostare la stessa opzione delle **righe da analizzare** nella finestra di dialogo di installazione.|  
|READONLY|TRUE per rendere di sola lettura il file; FALSE per fare in modo che il file non sia di sola lettura.<br /><br /> Viene impostata la stessa opzione di **sola lettura** nella finestra di dialogo di installazione.|  
|THREAD|Numero di thread in background per il motore da usare. Per il driver Microsoft Access, il valore predefinito è 3, ma è possibile modificarlo. Per dBASE, MicrosoftExceldriver questo valore è 3 e non può essere modificato.<br /><br /> Consente di impostare la stessa opzione dei **thread** nella finestra di dialogo di installazione.|
