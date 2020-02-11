---
title: Limitazioni dell'istruzione ALTER TABLE | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138427"
---
# <a name="alter-table-statement-limitations"></a>Limitazioni dell'istruzione ALTER TABLE
Quando si utilizza il driver dBASE o Paradox, dopo la creazione di un indice e l'aggiunta di un nuovo record, la struttura della tabella non può essere modificata dall'istruzione ALTER TABLE, a meno che l'indice non venga eliminato e il contenuto della tabella venga eliminato.  
  
 Le istruzioni ALTER TABLE non sono supportate per i driver di Microsoft Excel o di testo.  
  
> [!NOTE]  
>  Quando si utilizza il driver Paradox senza implementare il motore di database Borland, le istruzioni ALTER TABLE non sono supportate. sono consentite solo istruzioni Read e Append.
