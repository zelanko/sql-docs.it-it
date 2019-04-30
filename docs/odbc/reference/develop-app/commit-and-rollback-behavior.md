---
title: Comportamento di Rollback e commit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bad1706e7283c0b0a5111e93c9dfd7ae494c8ef4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63125497"
---
# <a name="commit-and-rollback-behavior"></a>Commit e comportamento di rollback
Un comportamento comune tra i server DBMS consiste nel chiudere i cursori e rimuovere le istruzioni preparate quando un'istruzione commit o rollback. I database desktop sono più possibilità di mantenere i cursori aperti e mantenere le istruzioni preparate. Per altre informazioni, vedere le opzioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR nel [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrizione della funzione e [effettiva delle transazioni su cursori e istruzioni preparate](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
