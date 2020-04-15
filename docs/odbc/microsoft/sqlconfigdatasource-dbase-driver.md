---
title: SQLConfigDataSource (driver dBASE) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18c6721b4f34772e8c3cd8e4f515233f80566fb3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283971"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (driver dBASE)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver dBASE. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La funzione **SQLConfigDataSource** utilizzata per aggiungere, modificare o eliminare un'origine dati in modo dinamico utilizza le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|CONFRONTOSEQUENZA|Sequenza in cui vengono ordinati i campi.<br /><br /> La sequenza può essere: ASCII (impostazione predefinita) o internazionale.<br /><br /> In questo modo viene impostata la stessa opzione della sequenza di **fascicolazione** nella finestra di dialogo di impostazione.|  
|DEFAULTDIR (DISE)|Specifica del percorso della directory.|  
|DELETED|Per il driver dBASE, specifica se le righe contrassegnate come eliminate possono essere recuperate o posizionate. Se impostato su 1, le righe eliminate non vengono visualizzate; se impostato su 0, le righe eliminate vengono considerate come le righe non eliminate.<br /><br /> Viene impostata la stessa opzione **Mostra righe eliminate** nella finestra di dialogo di impostazione.|  
|DESCRIZIONE|Descrizione dei dati nell'origine dati.<br /><br /> In questo modo viene impostata la stessa opzione **Descrizione** nella finestra di dialogo di installazione.|  
|DRIVER|Specifica del percorso della DLL del driver.|  
|DRIVERID|Un ID intero per il driver.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|Fil|Tipo di file dBase III, dBase IV o dBase 5|  
|Pagetimeout|Specifica il periodo di tempo, in decimi di secondo, in cui una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Il valore predefinito è 600 decimi di secondo (60 secondi). Si noti che questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> In questo modo viene impostata la stessa opzione di **Timeout pagina** nella finestra di dialogo di configurazione.|  
|READONLY|TRUE per rendere il file di sola lettura; FALSE per rendere il file non di sola lettura.<br /><br /> In questo modo viene impostata la stessa opzione **Sola lettura** nella finestra di dialogo di installazione.|  
|STATISTICS|Per il driver dBASE, determina se le statistiche sulle dimensioni della tabella sono approssimate. Si noti che questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> In questo modo viene impostata la stessa opzione del **conteggio righe approssimativo** nella finestra di dialogo di impostazione.|  
|Discussioni|Numero di thread in background per il motore da utilizzare. Questo valore è 3 e non può essere modificato.<br /><br /> In questo modo viene impostata la stessa opzione **di Thread** nella finestra di dialogo di installazione.|
