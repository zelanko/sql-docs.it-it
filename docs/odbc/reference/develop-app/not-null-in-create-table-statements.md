---
title: NOT NULL nelle istruzioni CREATE TABLE Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 490f4a7e49acdad5f919ad21f93d479b03099eb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302389"
---
# <a name="not-null-in-create-table-statements"></a>Istruzioni NOT NULL in CREATE TABLE
Alcuni database, e in particolare i database desktop, non supportano il vincolo di colonna **NOT NULL** nelle istruzioni **CREATE TABLE.** Per altre informazioni, vedere l'opzione SQL_NON_NULLABLE_COLUMNS nella descrizione della funzione [SQLGetInfo.For](../../../odbc/reference/syntax/sqlgetinfo-function.md) more information, see the SQL_NON_NULLABLE_COLUMNS option in the SQLGetInfo function description.
