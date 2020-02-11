---
title: Restituzione di SQL_NO_DATA | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2613593d9c2e20d5dfa01c0a0b4f9886dbc8e889
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057128"
---
# <a name="returning-sql_no_data"></a>Restituzione di SQL_NO_DATA
Quando un'applicazione *ODBC 2. x* con un driver ODBC *3. x* chiama **SQLExecDirect**, **SQLExecute**o **SQLParamData**e un'istruzione Update o DELETE ricercata è stata eseguita ma non ha interessato alcuna riga nell'origine dati, il driver ODBC *3. x* deve restituire SQL_SUCCESS. Quando un'applicazione *ODBC 3. x* che utilizza un driver ODBC *3. x* chiama **SQLExecDirect**, **SQLExecute**o **SQLParamData** con lo stesso risultato, il driver ODBC *3. x* deve restituire SQL_NO_DATA.  
  
 Se un'istruzione Update o DELETE cercata in un batch di istruzioni non influisce su alcuna riga nell'origine dati, **SQLMoreResults** restituisce SQL_SUCCESS. Non può restituire SQL_NO_DATA, perché ciò significa che non sono presenti altri risultati, non che è stato generato un risultato da un aggiornamento o da un'eliminazione ricercata che non ha interessato alcuna riga.
