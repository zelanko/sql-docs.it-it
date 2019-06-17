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
manager: craigg
ms.openlocfilehash: 02ce530385cdc911250a81d831dd2fdb81873f76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301983"
---
# <a name="alter-table-statement-limitations"></a>Limitazioni dell'istruzione ALTER TABLE
Quando il file dBASE o driver Paradox viene utilizzato, una volta che un indice è stato creato e aggiunto un nuovo record, la struttura della tabella non venga modificata dall'istruzione ALTER TABLE, a meno che l'indice viene eliminato e il contenuto della tabella viene eliminato.  
  
 Le istruzioni ALTER TABLE non sono supportate per i driver di Microsoft Excel o di testo.  
  
> [!NOTE]  
>  Quando si usa il driver Paradox senza implementare il motore di Database Borland, le istruzioni ALTER TABLE non sono supportate. solo lettura e aggiungere le istruzioni sono consentite.
