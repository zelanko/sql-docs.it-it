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
ms.openlocfilehash: 23823e53e516324832c79706e6171b48a9c5297c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071866"
---
# <a name="drop-index-statement"></a>Istruzione DROP INDEX
Quando viene usato il driver Paradox, dBASE o Microsoft Access, la sintassi dell'istruzione DROP INDEX è "DROP INDEX a in b" dove "a" è il nome dell'indice e "b" è il nome della tabella (non DROP INDEX *-nome dell'indice*).  
  
 Quando viene usato il driver Paradox, l'istruzione DROP INDEX Elimina i file di indice secondario Paradox.  
  
 L'istruzione DROP INDEX non è supportata per i driver di Microsoft Excel o di testo.
