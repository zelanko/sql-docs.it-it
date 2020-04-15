---
title: Limitazioni dell'istruzione UPDATE Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ddf19c0b672901b2e778833f8bf624996d4ced3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307622"
---
# <a name="update-statement-limitations"></a>Limitazioni dell'istruzione UPDATE
Affinché il driver Paradox aggiorni una tabella, la tabella deve avere un indice univoco (chiave primaria di Paradox). Quando si utilizza il driver Paradox senza implementare il motore di database Borland, non è possibile aggiornare una tabella di Paradox.  
  
 Non supportato dal driver di testo.  
  
 Quando si utilizza il driver di Microsoft Excel, è possibile aggiornare i valori, ma una riga non può essere eliminata da una tabella basata su un foglio di calcolo di Microsoft Excel. Di conseguenza, l'istruzione UPDATE non è considerata ufficialmente supportata dal driver di Microsoft Excel. Solo l'istruzione INSERT è considerata supportata.
