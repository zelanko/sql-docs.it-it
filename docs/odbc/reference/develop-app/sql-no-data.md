---
title: proprietà SQL_NO_DATA . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a399a270eb1cd2f3daf9449c53b1f577a6b9545
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299791"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
Quando un ODBC 3. *L'applicazione x* chiama **SQLExecDirect**, **SQLExecute**o **SQLParamData** in un file ODBC 2. *x* driver per eseguire un'istruzione di aggiornamento o eliminazione ricercata che non influisce sulle righe nell'origine dati, il driver deve restituire SQL_SUCCESS, non SQL_NO_DATA. Quando un ODBC 2. *x* o ODBC 3. *x* che utilizza un'applicazione ODBC 3. *x* driver chiama **SQLExecDirect**, **SQLExecute**, o **SQLParamData** con lo stesso risultato, ODBC 3. *x* driver deve restituire SQL_NO_DATA.
