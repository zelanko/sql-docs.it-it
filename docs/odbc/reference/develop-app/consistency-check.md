---
title: Controllo di coerenza - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: edd946ca865cd9d8d2edff2c7bedbb3b2629c97c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299001"
---
# <a name="consistency-check"></a>Verifica della coerenza
Una verifica di coerenza viene eseguita automaticamente dal driver ogni volta che un'applicazione imposta il campo SQL_DESC_DATA_PTR di APD, ARD o IPD. Ogni volta che questo campo è impostato, il driver verifica che il valore del campo SQL_DESC_TYPE e i valori applicabili al campo SQL_DESC_TYPE nello stesso record siano validi e coerenti.  
  
 Il campo SQL_DESC_DATA_PTR di un IPD non è normalmente impostato; tuttavia, un'applicazione può farlo per forzare una verifica di coerenza dei campi IPD. Il valore su cui è impostato il campo SQL_DESC_DATA_PTR dell'IPD non è effettivamente archiviato e non può essere recuperato da una chiamata a **SQLGetDescField** o **SQLGetDescRec;** l'impostazione viene effettuata solo per forzare la verifica della coerenza. Non è possibile eseguire una verifica di coerenza su un IRD.  
  
 Per ulteriori informazioni sulla verifica di coerenza, vedere [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).
