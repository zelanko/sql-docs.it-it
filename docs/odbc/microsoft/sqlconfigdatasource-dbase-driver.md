---
description: SQLConfigDataSource (driver dBASE)
title: SQLConfigDataSource (driver dBASE) | Microsoft Docs
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
ms.openlocfilehash: 23e734c5aafc903e210eea18f002f4c5e8d7a456
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411957"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (driver dBASE)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver dBASE. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La funzione **SQLConfigDataSource** utilizzata per aggiungere, modificare o eliminare un'origine dati in modo dinamico utilizza le parole chiave seguenti.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|Sequenza in cui vengono ordinati i campi.<br /><br /> La sequenza può essere: ASCII (impostazione predefinita) o internazionale.<br /><br /> In questo modo viene impostata la stessa opzione della **sequenza di ordinamento** nella finestra di dialogo di installazione.|  
|DEFAULTDIR|Specifica del percorso della directory.|  
|DELETED|Per il driver dBASE, specifica se è possibile recuperare o posizionare le righe contrassegnate come eliminate. Se impostato su 1, le righe eliminate non vengono visualizzate. Se impostato su 0, le righe eliminate vengono gestite come righe non eliminate.<br /><br /> Viene impostata la stessa opzione **Mostra righe eliminate** nella finestra di dialogo del programma di installazione.|  
|DESCRIZIONE|Descrizione dei dati nell'origine dati.<br /><br /> Questa opzione consente di impostare la stessa opzione della **Descrizione** nella finestra di dialogo di installazione.|  
|DRIVER|Specifica del percorso per la DLL del driver.|  
|DRIVERID|ID di tipo integer per il driver.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5,0)|  
|FIL|Tipo di file dBase III, dBase IV o dBase 5|  
|PAGETIMEOUT|Specifica il periodo di tempo, in decimi di secondo, che una pagina (se non utilizzata) rimane nel buffer prima di essere rimossa. Il valore predefinito è 600 decimi di secondo (60 secondi). Si noti che questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> In questo modo viene impostata la stessa opzione del **timeout della pagina** nella finestra di dialogo di installazione.|  
|READONLY|TRUE per rendere di sola lettura il file; FALSE per fare in modo che il file non sia di sola lettura.<br /><br /> Viene impostata la stessa opzione di **sola lettura** nella finestra di dialogo di installazione.|  
|STATISTICS|Per il driver dBASE, determina se le statistiche sulle dimensioni della tabella sono approssimate. Si noti che questa opzione si applica a tutte le origini dati che utilizzano il driver ODBC.<br /><br /> In questo modo viene impostata la stessa opzione del **numero di righe approssimativo** nella finestra di dialogo di installazione.|  
|THREAD|Numero di thread in background per il motore da usare. Questo valore è 3 e non può essere modificato.<br /><br /> Consente di impostare la stessa opzione dei **thread** nella finestra di dialogo di installazione.|
