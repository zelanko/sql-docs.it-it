---
title: Applicazioni e driver conformi agli standard | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b4daf2e777b20b1b84c090757d0d84796a4cae1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299718"
---
# <a name="standards-compliant-applications-and-drivers"></a>Applicazioni e driver conformi agli standard
Un driver o un'applicazione conforme agli standard è conforme alla specifica CAE del gruppo aperto "Gestione dati: interfaccia della riga di comando di SQL (CLI)" e all'interfaccia a livello di chiamata ISO/IEC 9075-3:1995 (E) (SQL/CLI).  
  
 ODBC *3. x* garantisce le funzionalità seguenti:  
  
-   Un'applicazione scritta nelle specifiche dell'interfaccia della riga di comando ISO e del gruppo aperto funzionerà con un driver ODBC *3. x* o un driver conforme agli standard quando viene compilato con i file di intestazione ODBC *3. x* e collegato alle librerie ODBC 3 *.* x e quando ottiene l'accesso al driver tramite Gestione driver ODBC *3. x* .  
  
-   Un driver scritto nelle specifiche dell'interfaccia della riga di comando ISO e del gruppo aperto funzionerà con un'applicazione ODBC *3. x* o un'applicazione conforme agli standard quando viene compilata con i file di intestazione ODBC *3. x* e collegata alle librerie ODBC *3.* x e quando l'applicazione ottiene l'accesso al driver tramite Gestione driver ODBC *3. x* .  
  
 I driver e le applicazioni conformi agli standard vengono compilati con il flag di compilazione ODBC_STD.  
  
 Le applicazioni conformi agli standard presentano il comportamento seguente:  
  
-   Se un'applicazione conforme agli standard chiama **SQLAllocEnv** (che può verificarsi perché **SQLAllocEnv** è una funzione valida nel gruppo Open e nell'interfaccia della riga di comando ISO), la chiamata viene mappata a **SQLAllocHandleStd** in fase di compilazione. Di conseguenza, in fase di esecuzione, l'applicazione chiama **SQLAllocHandleStd**. Durante l'elaborazione della chiamata, gestione driver imposta l'attributo SQL_ATTR_ODBC_VERSION Environment su SQL_OV_ODBC3. Una chiamata a **SQLAllocHandleStd** equivale a una chiamata a **SQLAllocHandle** con *HandleType* di SQL_HANDLE_ENV e una chiamata a **SQLSetEnvAttr** per impostare SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3.  
  
-   Se un'applicazione conforme agli standard chiama **SQLBindParam** (che può verificarsi perché **SQLBindParam** è una funzione valida nel gruppo Open e nell'interfaccia della riga di comando ISO), gestione driver ODBC *3. x* esegue il mapping della chiamata alla chiamata equivalente in **SQLBindParameter**. Per la compatibilità con le versioni precedenti, vedere [mapping di SQLBindParam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) in Appendice G: linee guida sui driver.  
  
-   Per l'allineamento con l'interfaccia della riga di comando ISO, i file di intestazione ODBC *3. x* contengono alias per i tipi di informazioni usati nelle chiamate a **SQLGetInfo**. Un'applicazione conforme agli standard può utilizzare questi alias anziché i tipi di informazioni ODBC *3. x* . Per ulteriori informazioni, vedere l'argomento successivo relativo ai [file di intestazione](../../../odbc/reference/develop-app/header-files.md).  
  
-   Un'applicazione conforme agli standard deve verificare che tutte le funzionalità supportate siano supportate nel driver che funzionerà con. L'impostazione dell'attributo SQL_ATTR_CURSOR_SCROLLABLE Statement su SQL_SCROLLABLE e sull'impostazione dell'attributo SQL_ATTR_CURSOR_SENSITIVITY Statement su SQL_INSENSITIVE o SQL_SENSITIVE sono le funzionalità disponibili come funzionalità facoltative negli standard, ma che non sono incluse nel livello principale ODBC *3. x* e pertanto potrebbero non essere supportate da tutti i driver ODBC *3. x* . Se un'applicazione conforme agli standard utilizza queste funzionalità, deve verificare che il driver che utilizzerà li supporti.
