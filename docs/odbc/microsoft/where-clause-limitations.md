---
title: In cui limitazioni della clausola | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, WHERE clause limitations
- WHERE clause limitations [ODBC]
ms.assetid: 46b54f74-e4a3-4318-87cf-8a97c38a2718
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e883d585db0fe11e92b188b2cfc26db9fff415fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057772"
---
# <a name="where-clause-limitations"></a>Limitazioni della clausola WHERE
Il numero massimo di clausole in una clausola WHERE è 40.  
  
 LONGVARCHAR e LONGVARBINARY colonne possono essere confrontati con i valori letterali di fino a 255 caratteri, ma non possono essere confrontate utilizzando i parametri.
