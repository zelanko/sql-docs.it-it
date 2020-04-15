---
title: Modifiche comportamentali e driver ODBC 3.x Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8343573261d74a6a0c652cf425b12da91f7cb0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292365"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>Modifiche del comportamento e driver ODBC 3.x
Attributo di ambiente SQL_ATTR_ODBC_VERSION indica al driver se è necessario presentare il comportamento ODBC *2.x* o ODBC *3.x.* La modalità di impostazione dell'attributo di ambiente SQL_ATTR_ODBC_VERSION dipende dall'applicazione. Le applicazioni ODBC *3.x* devono chiamare **SQLSetEnvAttr** per impostare questo attributo dopo aver chiamato **SQLAllocHandle** per allocare un handle di ambiente e prima di chiamare **SQLAllocHandle** per allocare un handle di connessione. In caso contrario, Gestione Driver restituisce SQLSTATE HY010 (errore di sequenza di funzione) su quest'ultima chiamata a **SQLAllocHandle**.  
  
> [!NOTE]  
>  Per ulteriori informazioni sulle modifiche comportamentali e sull'applicazione, vedere [Modifiche comportamentali](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Le applicazioni ODBC *2.x* e ODBC *2.x* ricompilate con i file di intestazione ODBC *3.x* non chiamano **SQLSetEnvAttr**. Tuttavia, chiamano **SQLAllocEnv** anziché **SQLAllocHandle** per allocare un handle di ambiente. Pertanto, quando l'applicazione chiama **SQLAllocEnv** in Gestione Driver, Gestione Driver chiama **SQLAllocHandle** e **SQLSetEnvAttr** nel driver. Pertanto, i driver ODBC *3.x* possono sempre contare su questo attributo impostato.  
  
 Se un'applicazione conforme agli standard compilata con il ODBC_STD flag di compilazione chiama **SQLAllocEnv** (che può verificarsi perché **SQLAllocEnv** non è deprecato in ISO), la chiamata viene mappata a **SQLAllocHandleStd** in fase di compilazione. In fase di esecuzione, l'applicazione chiama **SQLAllocHandleStd**. Gestione Driver imposta l'attributo di ambiente SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3. Una chiamata a **SQLAllocHandleStd** equivale a una chiamata a **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_ENV e una chiamata a **SQLSetEnvAttr** per impostare SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC3.  
  
 In determinate architetture di driver, è necessario che il driver venga visualizzato come driver ODBC *2.x* o ODBC *3.x,* a seconda della connessione. Il driver in questo caso potrebbe non essere effettivamente un driver, ma un livello che si trova tra Gestione Driver e un altro driver. Ad esempio, potrebbe simulare un driver, ad esempio ODBC Spy. In un altro esempio, potrebbe fungere da gateway, ad esempio EDA/SQL. Per essere visualizzato come driver ODBC *3.x,* tale driver deve essere in grado di esportare **SQLAllocHandle**e per essere visualizzato come driver ODBC *2.x,* deve essere in grado di esportare **SQLAllocConnect**, **SQLAllocEnv**e **SQLAllocStmt**. Quando un ambiente, una connessione o un'istruzione deve essere allocata, Gestione Driver verifica se questo driver esporta **SQLAllocHandle**. Poiché il driver, Gestione Driver chiama **SQLAllocHandle** nel driver. Se il driver utilizza un driver ODBC *2.x,* il driver deve eseguire il mapping della chiamata a **SQLAllocHandle** a **SQLAllocConnect**, **SQLAllocEnv**o **SQLAllocStmt,** a seconda dei casi. Deve inoltre non eseguire alcuna operazione con la chiamata **SQLSetEnvAttr** quando si comporta come driver ODBC *2.x.*  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di dati datetime](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [Compatibilità con le versioni precedenti dei tipi di dati C](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [Segnalibri di lunghezza fissa](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [Supporto di SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [Restituzione di SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [Chiamata di SQLSetPos per inserire i dati](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [Caricamento per ordinale](../../../odbc/reference/appendixes/loading-by-ordinal.md)
