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
ms.openlocfilehash: 7f5fe5cf6aae0d5953cc82b845396dd4164c7fa3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139019"
---
# <a name="header-record"></a>Record di intestazione
I campi del record di intestazione contengono informazioni generali sull'esecuzione di una funzione, tra cui il codice restituito, il conteggio delle righe, il numero di record di stato e il tipo di istruzione eseguita. Il record di intestazione viene sempre creato a meno che la funzione non restituisca SQL_INVALID_HANDLE. Per un elenco completo dei campi nel record di intestazione, vedere la descrizione della funzione [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) .
