---
description: SQL_NO_DATA
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb81d6f1fce50a27aba203eec4b78648754010e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424573"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
Quando ODBC 3. *x* l'applicazione chiama **SQLExecDirect**, **SQLExecute**o **SQLParamData** in ODBC 2. driver *x* per eseguire un'istruzione di aggiornamento o eliminazione ricercata che non influisce su alcuna riga nell'origine dati, il driver deve restituire SQL_SUCCESS, non SQL_NO_DATA. Quando ODBC 2. *x* o ODBC 3. applicazione *x* che utilizza un ODBC 3. il driver *x* chiama **SQLExecDirect**, **SQLExecute**o **SQLParamData** con lo stesso risultato, ODBC 3. il driver *x* deve restituire SQL_NO_DATA.
