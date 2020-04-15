---
title: Restituzione di SQL_NO_DATA Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305112"
---
# <a name="returning-sql_no_data"></a>Restituzione di SQL_NO_DATA
Quando un'applicazione ODBC *2.x* che utilizza un driver ODBC *3.x* chiama **SQLExecDirect**, **SQLExecute**o **SQLParamData**e un'istruzione di aggiornamento o eliminazione ricercata è stata eseguita ma non ha effetto su alcuna riga nell'origine dati, il driver ODBC *3.x* deve restituire SQL_SUCCESS. Quando un'applicazione ODBC *3.x* che utilizza un driver ODBC *3.x* chiama **SQLExecDirect**, **SQLExecute**o **SQLParamData** con lo stesso risultato, il driver ODBC *3.x* deve restituire SQL_NO_DATA.  
  
 Se un'istruzione di aggiornamento o eliminazione in un batch di istruzioni non influisce sulle righe nell'origine dati, **SQLMoreResults** restituisce SQL_SUCCESS. Non può restituire SQL_NO_DATA, perché ciò significherebbe che non ci sono più risultati, non che c'è un risultato da un aggiornamento/eliminazione ricercato che non ha interessato alcuna riga.
