---
title: SQL_NO_DATA | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f899e7a034e1ec5fc967d834caad3a4ccc4caa1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041827"
---
# <a name="sqlnodata"></a>SQL_NO_DATA
Quando un'applicazione ODBC 3. *x* applicazione chiama **SQLExecDirect**, **SQLExecute**, oppure **SQLParamData** in un'API ODBC 2. *x* driver di eseguire un aggiornamento con ricerca o eliminare l'istruzione che non influiscono su tutte le righe nell'origine dati, il driver deve restituire SQL_SUCCESS, non SQL_NO_DATA. Quando un'applicazione ODBC 2. *x* o ODBC 3. *x* funziona con un'applicazione ODBC 3. *x* driver chiama **SQLExecDirect**, **SQLExecute**, oppure **SQLParamData** con lo stesso risultato, ODBC 3. *x* driver restituisca SQL_NO_DATA.
