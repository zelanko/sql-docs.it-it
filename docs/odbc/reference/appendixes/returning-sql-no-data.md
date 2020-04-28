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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e2c806edd5d5647e09c00975ad7207ee5c2c876
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305112"
---
# <a name="returning-sql_no_data"></a>Restituzione di SQL_NO_DATA
Quando un'applicazione *ODBC 2. x* con un driver ODBC *3. x* chiama **SQLExecDirect**, **SQLExecute**o **SQLParamData**e un'istruzione Update o DELETE ricercata è stata eseguita ma non ha interessato alcuna riga nell'origine dati, il driver ODBC *3. x* deve restituire SQL_SUCCESS. Quando un'applicazione *ODBC 3. x* che utilizza un driver ODBC *3. x* chiama **SQLExecDirect**, **SQLExecute**o **SQLParamData** con lo stesso risultato, il driver ODBC *3. x* deve restituire SQL_NO_DATA.  
  
 Se un'istruzione Update o DELETE cercata in un batch di istruzioni non influisce su alcuna riga nell'origine dati, **SQLMoreResults** restituisce SQL_SUCCESS. Non può restituire SQL_NO_DATA, perché ciò significa che non sono presenti altri risultati, non che è stato generato un risultato da un aggiornamento o da un'eliminazione ricercata che non ha interessato alcuna riga.
