---
title: Record di intestazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7b6ffacb618dd2b7714be59814f3f1a88a52228
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208485"
---
# <a name="header-record"></a>Record di intestazione
I campi del record di intestazione contengono informazioni generali sull'esecuzione di una funzione, inclusi il codice restituito, conteggio delle righe, numero di record di stato e tipo di istruzione eseguita. Il record di intestazione viene sempre creato, a meno che la funzione non restituisca SQL_INVALID_HANDLE. Per un elenco completo dei campi del record di intestazione, vedere la [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descrizione della funzione.
