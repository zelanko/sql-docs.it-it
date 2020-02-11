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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041827"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
Quando ODBC 3. *x* l'applicazione chiama **SQLExecDirect**, **SQLExecute**o **SQLParamData** in ODBC 2. driver *x* per eseguire un'istruzione di aggiornamento o eliminazione ricercata che non influisce su alcuna riga nell'origine dati, il driver deve restituire SQL_SUCCESS, non SQL_NO_DATA. Quando ODBC 2. *x* o ODBC 3. applicazione *x* che utilizza un ODBC 3. il driver *x* chiama **SQLExecDirect**, **SQLExecute**o **SQLParamData** con lo stesso risultato, ODBC 3. il driver *x* deve restituire SQL_NO_DATA.
