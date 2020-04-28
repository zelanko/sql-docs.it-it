---
title: Comportamento di commit e rollback | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c67c29b295160a2908152b22c7a349ce4c0f9f50
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299131"
---
# <a name="commit-and-rollback-behavior"></a>Commit e comportamento di rollback
Un comportamento comune tra i DBMS del server consiste nel chiudere i cursori ed eliminare le istruzioni preparate quando viene eseguito il commit o il rollback di un'istruzione. Per i database desktop è più probabile che i cursori rimangano aperti e mantengano istruzioni preparate. Per ulteriori informazioni, vedere le opzioni SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR nella descrizione della funzione [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) ed [effetto delle transazioni sui cursori e sulle istruzioni preparate](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
