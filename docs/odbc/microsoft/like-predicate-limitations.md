---
title: Limitazioni del predicato LIKE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8035eed9e0aaff1f914f386b6d4bc9f2d65f9a0f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192357"
---
# <a name="like-predicate-limitations"></a>Limitazioni del predicato LIKE
Se i dati in una colonna sono più lunghi di 255 caratteri, il confronto tra LIKE baserà solo i primi 255 caratteri.  
  
 Un tipo usato in una routine è supportata solo con modelli costanti. I driver di Database Desktop supportano SQL-92, ad esempio criteri di ricerca.  
  
 Utilizzo di una clausola di escape in un predicato LIKE non è supportato.  
  
 Non è necessario eseguire un confronto LIKE su una colonna contenente i dati di un tipo di dati numerici o float. I risultati potrebbero essere imprevedibili. Per altre informazioni, vedere la *Guida per programmatori di Microsoft Jet Database Engine*.
