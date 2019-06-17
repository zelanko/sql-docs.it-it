---
title: Applicazioni conformi agli standard e driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8937c2b9c80209975d03963acb19ab5da9c99e39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63148908"
---
# <a name="standards-compliant-applications-and-drivers"></a>Applicazioni e driver conformi agli standard
Un'applicazione conforme agli standard o un driver è quella più conforme alla specifica CAE gruppo Open "gestione dei dati: SQL a livello di chiamata Interface (CLI)"e ISO/IEC 9075-3:1995 (E) a livello di chiamata CLI (interfaccia SQL /).  
  
 ODBC 3*x* garantisce le caratteristiche seguenti:  
  
-   Un'applicazione scritta in base alle specifiche Open Group e ISO CLI funzionerà con un'applicazione ODBC 3 *. x* driver o un driver conforme agli standard quando viene compilato con ODBC 3*x* intestazione file, con collegamenti e ODBC 3 *. x* librerie, e quando riesce ad accedere al driver tramite ODBC 3*x* gestione Driver.  
  
-   Un driver scritto in base alle specifiche Open Group e ISO CLI funzionerà con un'applicazione ODBC 3 *. x* applicazione o un'applicazione conforme agli standard quando viene compilato con ODBC 3*x* i file di intestazione e collegato con ODBC 3 *. x* librerie, e quando l'applicazione può accedere al driver tramite ODBC 3*x* gestione Driver.  
  
 Driver e conforme agli standard delle applicazioni vengono compilate con il flag di compilazione ODBC_STD.  
  
 Le applicazioni conformi agli standard mostrano il comportamento seguente:  
  
-   Se un'applicazione conforme agli standard chiama **SQLAllocEnv** (che può verificarsi poiché **SQLAllocEnv** è una funzione valida nel Open Group e ISO CLI), la chiamata viene mappata a  **SQLAllocHandleStd** in fase di compilazione. Di conseguenza, in fase di esecuzione, l'applicazione chiama **SQLAllocHandleStd**. Nel corso dell'elaborazione di questa chiamata, gestione Driver imposta l'attributo di ambiente SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3. Una chiamata a **SQLAllocHandleStd** equivale a una chiamata a **SQLAllocHandle** con un *HandleType* SQL_HANDLE_ENV e una chiamata a **SQLSetEnvAttr** per impostare SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3.  
  
-   Se un'applicazione conforme agli standard chiama **SQLBindParam** (che può verificarsi poiché **SQLBindParam** è una funzione valida nel Open Group e ISO CLI), ODBC 3*x* La chiamata a chiamata di equivalenti in esegue il mapping di Gestione driver **SQLBindParameter**. (Vedere [Mapping di SQLBindParam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti.)  
  
-   In modo da allinearsi con la CLI di ISO, ODBC 3 *. x* file di intestazione contengono alias per i tipi di informazioni usati nelle chiamate a **SQLGetInfo**. Un'applicazione conforme agli standard può usare questi alias anziché di ODBC 3*x* tipi di informazioni. Per altre informazioni, vedere l'argomento successivo [file di intestazione](../../../odbc/reference/develop-app/header-files.md).  
  
-   Un'applicazione conforme agli standard è necessario verificare che tutte le funzionalità che supporta sono supportate nel driver che funzionerà con. Impostare l'attributo di istruzione SQL_ATTR_CURSOR_SCROLLABLE su SQL_SCROLLABLE e impostando l'attributo di istruzione SQL_ATTR_CURSOR_SENSITIVITY su SQL_SENSITIVE o SQL_INSENSITIVE sono funzionalità che sono disponibili come funzioni facoltative negli standard ma non sono inclusi in ODBC 3 *. x* Core livello e pertanto potrebbe non essere supportati da tutti i 3 ODBC*x* driver. Se un'applicazione conforme agli standard Usa queste funzionalità, è necessario verificare che il driver che funzionerà con supportarle.
