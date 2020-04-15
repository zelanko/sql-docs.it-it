---
title: proprietà SQL_ARD_TYPE . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7e28d6babb7db8364697ae62092256396b44914
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305032"
---
# <a name="sql_ard_type"></a>SQL_ARD_TYPE
L'identificatore di tipo SQL_ARD_TYPE viene utilizzato per indicare che i dati in un buffer saranno del tipo specificato nel campo SQL_DESC_CONCISE_TYPE dell'ARD. SQL_ARD_TYPE viene immessa nell'argomento *TargetType* di una chiamata a **SQLGetData** anziché a un tipo di dati specifico e consente a un'applicazione di modificare il tipo di dati del buffer modificando il campo del descrittore. Questo valore collega il * \** tipo di dati del buffer TargetValuePtr al campo del descrittore. (SQL_ARD_TYPE non viene immesso in una chiamata a **SQLBindCol** o **SQLBindParameter** perché il tipo del buffer associato è già legato ai campi SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE e può essere modificato in qualsiasi momento modificando uno di questi campi.)  
  
 L'identificatore di tipo SQL_ARD_TYPE può essere utilizzato per specificare valori non predefiniti per la precisione iniziale e la precisione dei secondi dei tipi di dati intervallo e i valori di precisione e scala per il tipo di dati SQL_C_NUMERIC. Per ulteriori informazioni, vedere [Precisione dell'interlinea e dei secondi predefinita per i tipi di dati a intervalli](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) e [Precisione e scala predefinite per](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)i tipi di dati numerici , più avanti in questa appendice.
