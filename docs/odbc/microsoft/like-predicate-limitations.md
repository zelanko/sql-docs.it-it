---
title: Limitazioni del predicato di LIKE Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d596d688956d7bdbf3d9125184d81c16249781c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298961"
---
# <a name="like-predicate-limitations"></a>Limitazioni del predicato LIKE
Se i dati in una colonna sono più lunghi di 255 caratteri, il confronto LIKE sarà basato solo sui primi 255 caratteri.  
  
 Un'usA utilizzata in una routine è supportata solo con modelli costanti. I driver di database desktop supportano i criteri di ricerca LIKE di SQL-92.  
  
 L'utilizzo di una clausola di escape in un predicato LIKE non è supportato.  
  
 Un confronto LIKE non deve essere eseguito su una colonna contenente dati di tipo numerico o float. I risultati possono essere imprevedibili. Per ulteriori informazioni, vedere *Microsoft Jet Database Engine Programmer's Guide*.
