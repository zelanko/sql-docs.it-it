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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 372185966cc1644147feb2683177ae3a5b69e788
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300181"
---
# <a name="header-record"></a>Record di intestazione
I campi del record di intestazione contengono informazioni generali sull'esecuzione di una funzione, tra cui il codice restituito, il conteggio delle righe, il numero di record di stato e il tipo di istruzione eseguita. Il record di intestazione viene sempre creato a meno che la funzione non restituisca SQL_INVALID_HANDLE. Per un elenco completo dei campi nel record di intestazione, vedere la descrizione della funzione [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) .
