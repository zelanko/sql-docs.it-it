---
title: SQLConfigDataSource (driver file di testo) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283921"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (driver file di testo)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver del file di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La funzione **SQLConfigDataSource** utilizzata per aggiungere, modificare o eliminare un'origine dati in modo dinamico utilizza le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|CHARACTERSET|Per il driver di testo, OEM o ANSI.|  
|COLNAMEHEADER|Per il driver di testo, indica se il primo record di dati specifica i nomi delle colonne. TRUE o FALSE.|  
|DEFAULTDIR|Specifica del percorso della directory.|  
|DESCRIZIONE|Descrizione dei dati nell'origine dati.<br /><br /> Questa opzione consente di impostare la stessa opzione della **Descrizione** nella finestra di dialogo di installazione.|  
|DRIVER|Specifica del percorso per la DLL del driver.|  
|DRIVERID|ID di tipo integer per il driver. 27 (testo)|  
|ESTENSIONI|Elenca le estensioni dei nomi di file di testo nell'origine dati.<br /><br /> Consente di impostare la stessa opzione dell' **elenco di estensioni** nella finestra di dialogo di installazione.|  
|FIL|Testo tipo di file|  
|FILETYPE|Tipo di file per il driver di testo (testo).|  
|FORMAT|Per il driver di testo, può essere FIXEDLENGTH, TABDELIMITED, CSVDELIMITED (tramite una virgola) o delimitato () (dal carattere speciale specificato nelle parentesi). Il carattere speciale è di un carattere di lunghezza e può essere in formato carattere, decimale o esadecimale.|  
|MAXSCANROWS|Numero di righe da analizzare quando si imposta il tipo di dati di una colonna in base ai dati esistenti.<br /><br /> Per il driver di testo, è possibile immettere un numero compreso tra 1 e 32767 per il numero di righe da analizzare. Tuttavia, il valore predefinito è sempre 25. (Un numero al di fuori del limite restituirà un errore).<br /><br /> Consente di impostare la stessa opzione delle **righe da analizzare** nella finestra di dialogo di installazione.|  
|READONLY|TRUE per rendere di sola lettura il file; FALSE per fare in modo che il file non sia di sola lettura.<br /><br /> Viene impostata la stessa opzione di **sola lettura** nella finestra di dialogo di installazione.|
