---
title: Applicazioni e driver conformi agli standard Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299718"
---
# <a name="standards-compliant-applications-and-drivers"></a>Applicazioni e driver conformi agli standard
Un'applicazione o un driver conforme agli standard di applicazione o a livello di chiamata (CLI)" e dell'interfaccia SQL/CLI (ISO/IEC 9075-3:1995) del livello di chiamata (SQL/CLI).  
  
 ODBC *3.x* garantisce le seguenti funzionalità:  
  
-   Un'applicazione scritta nelle specifiche Open Group e ISO CLI funzionerà con un driver ODBC *3.x* o un driver conforme agli standard quando viene compilata con i file di intestazione ODBC *3.x* e collegata alle librerie ODBC *3.x* e quando ottiene l'accesso al driver tramite Gestione driver ODBC *3.x.*  
  
-   Un driver scritto nelle specifiche Open Group e ISO CLI funzionerà con un'applicazione ODBC *3.x* o un'applicazione conforme agli standard quando viene compilata con i file di intestazione ODBC *3.x* e collegata alle librerie ODBC *3.x* e quando l'applicazione ottiene l'accesso al driver tramite Gestione driver ODBC *3.x.*  
  
 Le applicazioni e i driver conformi agli standard vengono compilati con il flag di compilazione ODBC_STD.  
  
 Le applicazioni conformi agli standard presentano il seguente comportamento:  
  
-   Se un'applicazione conforme agli standard chiama **SQLAllocEnv** (che può verificarsi perché **SQLAllocEnv** è una funzione valida nel gruppo aperto e nell'interfaccia della riga di comando ISO), la chiamata viene mappata a **SQLAllocHandleStd** in fase di compilazione. Di conseguenza, in fase di esecuzione, l'applicazione chiama **SQLAllocHandleStd**. Durante l'elaborazione di questa chiamata, Gestione Driver imposta l'attributo di ambiente SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3. Una chiamata a **SQLAllocHandleStd** equivale a una chiamata a **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_ENV e una chiamata a **SQLSetEnvAttr** per impostare SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3.  
  
-   Se un'applicazione conforme agli standard chiama **SQLBindParam** (che può verificarsi perché **SQLBindParam** è una funzione valida nel gruppo aperto e nell'interfaccia della riga di comando ISO), Gestione Driver ODBC *3.x* esegue il mapping della chiamata alla chiamata equivalente in **SQLBindParameter**. Vedere [Mapping SQLBindParam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) nell'appendice G: Linee guida per i driver per la compatibilità con le versioni precedenti.  
  
-   Per allinearsi all'interfaccia della riga di comando ISO, i file di intestazione ODBC *3.x* contengono alias per i tipi di informazioni utilizzati nelle chiamate a **SQLGetInfo**. Un'applicazione conforme agli standard può utilizzare questi alias anziché i tipi di informazioni ODBC *3.x.* Per ulteriori informazioni, vedere l'argomento successivo, File di [intestazione](../../../odbc/reference/develop-app/header-files.md).  
  
-   Un'applicazione conforme agli standard deve verificare che tutte le funzionalità supportate siano supportate nel driver con cui funzionerà. L'impostazione dell'attributo dell'istruzione SQL_ATTR_CURSOR_SCROLLABLE su SQL_SCROLLABLE e l'impostazione dell'attributo di istruzione SQL_ATTR_CURSOR_SENSITIVITY su SQL_INSENSITIVE o SQL_SENSITIVE sono funzionalità disponibili come funzionalità facoltative negli standard ma non incluse nel livello ODBC *3.x* Core e pertanto potrebbero non essere supportate da tutti i driver ODBC *3.x.* Se un'applicazione conforme agli standard utilizza queste funzionalità, deve verificare che il driver con cui funzionerà le supporti.
