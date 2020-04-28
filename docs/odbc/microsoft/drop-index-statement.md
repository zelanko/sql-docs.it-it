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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 638bae6491c020519a0123ff56fe31e9a9ca1cf7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303432"
---
# <a name="drop-index-statement"></a>Istruzione DROP INDEX
Quando si usa il driver Microsoft Access, dBASE o Paradox, la sintassi dell'istruzione DROP INDEX è "DROP INDEX a on b", dove "a" è il nome dell'indice e "b" è il nome della tabella (non DROP INDEX *index-name*).  
  
 Quando si utilizza il driver Paradox, l'istruzione DROP INDEX Elimina i file di indice secondario Paradox.  
  
 L'istruzione DROP INDEX non è supportata per i driver di Microsoft Excel o di testo.
