---
title: Driver Unicode - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aabdd899d78c1141716725d57e343dc002dc96ad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284353"
---
# <a name="unicode-drivers"></a>Driver di Unicode
Se un driver deve essere un driver Unicode o un driver ANSI dipende interamente dalla natura dell'origine dati. Se l'origine dati supporta i dati Unicode, il driver deve essere un driver Unicode.If the data source supports Unicode data, the driver should be a Unicode driver. Se l'origine dati supporta solo dati ANSI, il driver deve rimanere un driver ANSI.  
  
 Un driver Unicode deve esportare **SQLConnectW** per essere riconosciuto come driver Unicode da Gestione Driver.  
  
 Un driver Unicode deve accettare funzioni Unicode (con un suffisso *W)* e archiviare i dati Unicode. Può anche accettare funzioni ANSI, ma non è necessario. Gestione Driver non passa una chiamata di funzione ANSI con il suffisso *A* al driver, ma lo converte in una chiamata di funzione ANSI senza il suffisso e quindi lo passa al driver.)  
  
 Un driver Unicode deve essere in grado di restituire set di risultati in Unicode o ANSI, a seconda dell'associazione dell'applicazione. Se un'applicazione viene associata a SQL_C_CHAR, il driver Unicode deve convertire i dati SQL_WCHAR in SQL_CHAR. Gestione driver esererà SQL_C_WCHAR a SQL_C_CHAR per i driver ANSI, ma non esegue alcuna mappatura per i driver Unicode.  
  
> [!NOTE]  
>  Quando si determina il tipo di driver, Gestione Driver chiamerà **SQLSetConnectAttr** e impostare il SQL_ATTR_ANSI_APP attributo in fase di connessione. Se l'applicazione utilizza le API ANSI, SQL_ATTR_ANSI_APP verrà impostata su SQL_AA_TRUE e, se utilizza Unicode, verrà impostata sul valore di SQL_AA_FALSE. Questo attributo viene utilizzato in modo che il driver possa presentare un comportamento diverso in base al tipo di applicazione. L'attributo non può essere impostato direttamente dall'applicazione e non è supportato da **SQLGetConnectAttr**. Se un driver presenta lo stesso comportamento per entrambe le applicazioni ANSI e Unicode, deve restituire SQL_ERROR per questo attributo. Se il driver restituisce SQL_SUCCESS, Gestione Driver separerà le connessioni ANSI e Unicode quando viene utilizzato il pool di connessioni.
