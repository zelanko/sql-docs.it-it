---
description: Limitazioni dell'istruzione ALTER TABLE
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53f86e8d2c21fb6ea2d016610848773564d4a384
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449593"
---
# <a name="alter-table-statement-limitations"></a>Limitazioni dell'istruzione ALTER TABLE
Quando si utilizza il driver dBASE o Paradox, dopo la creazione di un indice e l'aggiunta di un nuovo record, la struttura della tabella non può essere modificata dall'istruzione ALTER TABLE, a meno che l'indice non venga eliminato e il contenuto della tabella venga eliminato.  
  
 Le istruzioni ALTER TABLE non sono supportate per i driver di Microsoft Excel o di testo.  
  
> [!NOTE]  
>  Quando si utilizza il driver Paradox senza implementare il motore di database Borland, le istruzioni ALTER TABLE non sono supportate. sono consentite solo istruzioni Read e Append.
