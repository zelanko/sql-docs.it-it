---
title: Istruzione DROP INDEX | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DROP INDEX [ODBC]
- SQL grammar [ODBC], DROP INDEX
ms.assetid: cd0ff767-9254-413b-bd1a-bed26c6774f5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b00f15f6a660025930ac401278a571f5cb617697
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128021"
---
# <a name="drop-index-statement"></a>Istruzione DROP INDEX
Quando viene usato il driver Paradox, dBASE o Microsoft Access, la sintassi dell'istruzione DROP INDEX è "DROP INDEX a in b" dove "a" è il nome dell'indice e "b" è il nome della tabella (non DROP INDEX *-nome dell'indice*).  
  
 Quando viene usato il driver Paradox, l'istruzione DROP INDEX Elimina i file di indice secondario Paradox.  
  
 L'istruzione DROP INDEX non è supportata per i driver di Microsoft Excel o di testo.
