---
title: SQLConfigDataSource (Driver File di testo) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 46bb00fb01ed3fee8098420794af089f2d8b981e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054079"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (driver file di testo)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver File di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il **SQLConfigDataSource** funzione che consente di aggiungere, modificare o eliminare un'origine dati utilizza in modo dinamico le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|CHARACTERSET|Per il driver di testo, OEM o ANSI.|  
|COLNAMEHEADER|Per il driver di testo, indica se il primo record di dati è necessario specificare i nomi delle colonne. TRUE o FALSE.|  
|DEFAULTDIR|La specifica del percorso della directory.|  
|DESCRIPTION|Una descrizione dei dati nell'origine dati.<br /><br /> Consente di impostare la stessa opzione come **descrizione** nella finestra di dialogo programma di installazione.|  
|DRIVER|Specifica il percorso alla DLL del driver.|  
|DRIVERID|Un ID intero per il driver. 27 (testo)|  
|ESTENSIONI|Elenca le estensioni dei file di testo sull'origine dati.<br /><br /> Consente di impostare la stessa opzione come **elenco di estensioni** nella finestra di dialogo programma di installazione.|  
|FIL|Tipo di file testo|  
|FILETYPE|Tipo di file per il driver di testo (testo).|  
|FORMAT|Per il driver di testo, può essere FIXEDLENGTH, TABDELIMITED, CSVDELIMITED (da una virgola) o DELIMITED() (dal carattere speciale specificato tra parentesi). Il carattere speciale è lunga un carattere e può essere in formato di carattere, decimale o esadecimale.|  
|MAXSCANROWS|Il numero di righe da analizzare quando si imposta il tipo di dati di una colonna in base ai dati esistenti.<br /><br /> Per il driver di testo, è possibile immettere un numero compreso tra 1 e 32767 per il numero di righe da analizzare; Tuttavia, il valore verrà sempre aperta a 25. (Un numero di fuori del limite verrà restituito un errore).<br /><br /> Consente di impostare la stessa opzione come **righe da analizzare** nella finestra di dialogo programma di installazione.|  
|READONLY|TRUE per rendere i file di sola lettura. FALSE per rendere i file non di sola lettura.<br /><br /> Consente di impostare la stessa opzione come **Read Only** nella finestra di dialogo programma di installazione.|
