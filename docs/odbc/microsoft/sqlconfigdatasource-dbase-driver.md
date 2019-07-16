---
title: SQLConfigDataSource (Driver dBASE) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 569a83110d7d5a3cd25eed8f68753d13793f8b10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054105"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (driver dBASE)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver dBASE. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Il **SQLConfigDataSource** funzione che consente di aggiungere, modificare o eliminare un'origine dati utilizza in modo dinamico le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|La sequenza nella quale vengono ordinati i campi.<br /><br /> La sequenza può essere: ASCII (predefinito) o internazionale.<br /><br /> Consente di impostare la stessa opzione come **sequenza di collazione** nella finestra di dialogo programma di installazione.|  
|DEFAULTDIR|La specifica del percorso della directory.|  
|DELETED|Per il driver dBASE, specifica se le righe che sono state contrassegnate come eliminati possono essere recuperate o posizionato in corrispondenza. Se impostato su 1, le righe eliminate non viene visualizzata. Se impostato su 0, righe eliminate viene trattate come righe non è stato eliminato.<br /><br /> Consente di impostare la stessa opzione come **Mostra le righe eliminate** nella finestra di dialogo programma di installazione.|  
|DESCRIPTION|Una descrizione dei dati nell'origine dati.<br /><br /> Consente di impostare la stessa opzione come **descrizione** nella finestra di dialogo programma di installazione.|  
|DRIVER|Specifica il percorso alla DLL del driver.|  
|DRIVERID|Un ID intero per il driver.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|File digitare dBase III, dBase IV o dBase 5|  
|PAGETIMEOUT|Specifica il periodo di tempo, in decimi di secondo, che una pagina, se non utilizzato, rimane nel buffer prima della rimozione. Il valore predefinito è 600 decimi di secondo (60 secondi). Si noti che questa opzione si applica a tutte le origini dati che usano il driver ODBC.<br /><br /> Consente di impostare la stessa opzione come **Page Timeout** nella finestra di dialogo programma di installazione.|  
|READONLY|TRUE per rendere i file di sola lettura. FALSE per rendere i file non di sola lettura.<br /><br /> Consente di impostare la stessa opzione come **Read Only** nella finestra di dialogo programma di installazione.|  
|STATISTICS|Per il driver dBASE, determina se le statistiche delle tabelle delle dimensioni sono approssimative. Si noti che questa opzione si applica a tutte le origini dati che usano il driver ODBC.<br /><br /> Consente di impostare la stessa opzione come **conteggio righe approssimative** nella finestra di dialogo programma di installazione.|  
|THREAD|Il numero di thread in background per il motore da usare. Questo valore è 3 e non può essere modificato.<br /><br /> Consente di impostare la stessa opzione come **thread** nella finestra di dialogo programma di installazione.|
