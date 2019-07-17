---
title: Limitazioni dell'istruzione ALTER nella tabella | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1333cd6cd5946b7a3a70152e12f4d3decfa7fed0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138427"
---
# <a name="alter-table-statement-limitations"></a>Limitazioni dell'istruzione ALTER TABLE
Quando il file dBASE o driver Paradox viene utilizzato, una volta che un indice è stato creato e aggiunto un nuovo record, la struttura della tabella non venga modificata dall'istruzione ALTER TABLE, a meno che l'indice viene eliminato e il contenuto della tabella viene eliminato.  
  
 Le istruzioni ALTER TABLE non sono supportate per i driver di Microsoft Excel o di testo.  
  
> [!NOTE]  
>  Quando si usa il driver Paradox senza implementare il motore di Database Borland, le istruzioni ALTER TABLE non sono supportate. solo lettura e aggiungere le istruzioni sono consentite.
