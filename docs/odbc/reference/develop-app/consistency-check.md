---
title: Verifica coerenza | Microsoft Docs
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
ms.openlocfilehash: 419e338a5e96821606dc26a53a4fccecbc72ae3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125526"
---
# <a name="consistency-check"></a>Verifica della coerenza
Una verifica della coerenza viene eseguita automaticamente dal driver ogni volta che un'applicazione imposta il campo SQL_DESC_DATA_PTR di APD, ARD o dip. Ogni volta che viene impostato questo campo, il driver verifica che il valore del campo SQL_DESC_TYPE e i valori applicabili al campo SQL_DESC_TYPE nello stesso record siano validi e coerenti.  
  
 Il campo SQL_DESC_DATA_PTR di un oggetto dpi non è impostato normalmente; Tuttavia, un'applicazione può eseguire questa operazione per forzare una verifica di coerenza dei campi di dpi. Il valore che il campo SQL_DESC_DATA_PTR di dpi è impostato su non è effettivamente archiviato e non può essere recuperato da una chiamata a **SQLGetDescField** o **SQLGetDescRec**; l'impostazione viene eseguita solo per forzare la verifica della coerenza. Non è possibile eseguire una verifica di coerenza su un IRD.  
  
 Per ulteriori informazioni sulla verifica della coerenza, vedere [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).
