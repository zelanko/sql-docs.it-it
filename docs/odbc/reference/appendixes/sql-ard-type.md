---
title: SQL_ARD_TYPE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 683b81f82094aa33deef86ffc19dc8c5c0a53a27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270441"
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
L'identificatore di tipo SQL_ARD_TYPE viene utilizzato per indicare che i dati in un buffer sarà del tipo specificato nel campo SQL_DESC_CONCISE_TYPE del ARD. SQL_ARD_TYPE viene immesso nel *TargetType* argomento di una chiamata a **SQLGetData** anziché un tipo di dati specifico e consente di digitare un'applicazione di modificare i dati del buffer, modificare il descrittore campo. Questo valore consente di associare il tipo di dati di  *\*TargetValuePtr* buffer per il campo di descrizione. (SQL_ARD_TYPE non viene immesso in una chiamata a **SQLBindCol** oppure **SQLBindParameter** perché il tipo di buffer associato è già associato ai campi SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE e può essere modificato in qualsiasi momento modificando uno di questi campi.)  
  
 L'identificatore del tipo SQL_ARD_TYPE consente di specificare valori non predefiniti per la precisione iniziale e la precisione dei secondi di tipi di dati intervallo e digitare i valori di precisione e scala per quelli SQL_C_NUMERIC. Per altre informazioni, vedere [viene sottoposto a override Default iniziali e la precisione in secondi per i tipi di dati di intervallo](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) e [override Default precisione e scala per i tipi di dati numerici](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md), più avanti in questa appendice.
