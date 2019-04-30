---
title: Verifica di coerenza | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb73d8a4de482f24eae5794232019af9890e3624
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043736"
---
# <a name="consistency-check"></a>Verifica della coerenza
Verifica di coerenza viene eseguita automaticamente dal driver ogni volta che un'applicazione imposta il campo SQL_DESC_DATA_PTR del APD, ARD o IPD. Ogni volta che questo campo è impostato, il driver verificherà che il valore del campo SQL_DESC_TYPE e i valori applicabili per il campo SQL_DESC_TYPE nello stesso record siano validi e coerenti.  
  
 Il campo SQL_DESC_DATA_PTR di un IPD non è in genere impostato; Tuttavia, un'applicazione può farlo per forzare un controllo di consistenza dei campi IPD. Il valore impostato per il campo SQL_DESC_DATA_PTR dell'IPD non viene effettivamente archiviato e non può essere recuperato da una chiamata a **SQLGetDescField** oppure **SQLGetDescRec**; l'impostazione viene eseguita solo per forzare il verifica della coerenza. Impossibile eseguire una verifica coerenza su un'implementazione.  
  
 Per ulteriori informazioni sulla verifica di coerenza, vedere [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).
