---
title: Modifiche del comportamento e driver ODBC 3.x | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27b48951c6fb3be8bfe070863409d77ab760d5fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915613"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>Modifiche del comportamento e driver ODBC 3.x
L'attributo di ambiente SQL_ATTR_ODBC_VERSION indica al driver, se è necessario presentare ODBC *2.x* comportamento o ODBC *3.x* comportamento. Come è impostato l'attributo di ambiente SQL_ATTR_ODBC_VERSION dipende dall'applicazione. ODBC *3.x* le applicazioni devono chiamare **SQLSetEnvAttr** per impostare questo attributo dopo che chiamano **SQLAllocHandle** per allocare un handle di ambiente e prima di chiamare  **SQLAllocHandle** per allocare un handle di connessione. Se non riescono a tale scopo, gestione Driver restituisce SQLSTATE HY010 (funzione di errore nella sequenza) alla chiamata a quest'ultima **SQLAllocHandle**.  
  
> [!NOTE]  
>  Per altre informazioni su modifiche del comportamento e come funziona un'applicazione, vedere [modifiche del comportamento](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 ODBC *2.x* ODBC e le applicazioni *2.x* le applicazioni ricompilate con ODBC *3.x* i file di intestazione non chiamano **SQLSetEnvAttr**. Tuttavia, essi richiamano **SQLAllocEnv** invece di **SQLAllocHandle** per allocare un handle di ambiente. Pertanto, quando l'applicazione chiama **SQLAllocEnv** in Gestione Driver, gestione Driver chiama **SQLAllocHandle** e **SQLSetEnvAttr** nel driver. Di conseguenza, ODBC *3.x* driver sempre possono contare su questo attributo da impostare.  
  
 Se un'applicazione conforme agli standard compilato con il flag di compilazione ODBC_STD chiamate **SQLAllocEnv** (che potrebbe verificarsi perché **SQLAllocEnv** non è stato deprecato in ISO), la chiamata viene mappata a  **SQLAllocHandleStd** in fase di compilazione. In fase di esecuzione, l'applicazione chiama **SQLAllocHandleStd**. Gestione Driver imposta l'attributo di ambiente SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3. Una chiamata a **SQLAllocHandleStd** equivale a una chiamata a **SQLAllocHandle** con un *HandleType* SQL_HANDLE_ENV e una chiamata a **SQLSetEnvAttr** per impostare SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3.  
  
 In alcune architetture di driver, è necessario per il driver venga visualizzato come un ODBC *2.x* driver o un database ODBC *3.x* driver, a seconda della connessione. Il driver in questo caso potrebbe non risultare un driver, ma un livello in cui si trova tra la gestione di Driver e un altro driver. Ad esempio, potrebbe simulare un driver, ad esempio ODBC Spy. In un altro esempio, può agire come gateway, come EDA/SQL. Vengono visualizzati come un database ODBC *3.x* driver, un driver di questo tipo deve essere in grado di esportare **SQLAllocHandle**e venga visualizzato come un database ODBC *2.x* driver, deve essere in grado di esportare  **SQLAllocConnect**, **SQLAllocEnv**, e **SQLAllocStmt**. Quando un ambiente, connessione o dell'istruzione deve essere allocato, gestione Driver controlla se questo driver Esporta **SQLAllocHandle**. Poiché il driver esegue, le chiamate di gestione Driver **SQLAllocHandle** nel driver. Se il driver collabora con un database ODBC *2.x* driver, il driver deve eseguire il mapping della chiamata a **SQLAllocHandle** al **SQLAllocConnect**, **SQLAllocEnv**, oppure **SQLAllocStmt**, nel modo appropriato. Anche necessario non eseguire alcuna operazione con il **SQLSetEnvAttr** chiamare quando si comporta come un database ODBC *2.x* driver.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di dati datetime](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [Compatibilità con le versioni precedenti dei tipi di dati C](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [Segnalibri di lunghezza fissa](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [Supporto di SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [Restituzione di SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [Chiamata di SQLSetPos per inserire i dati](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [Caricamento per ordinale](../../../odbc/reference/appendixes/loading-by-ordinal.md)
