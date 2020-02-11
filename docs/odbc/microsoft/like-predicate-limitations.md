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
ms.openlocfilehash: 8cd3cebfcf20df2f8a3a786ea66fd28dd76307c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68119714"
---
# <a name="like-predicate-limitations"></a>Limitazioni del predicato LIKE
Se i dati in una colonna hanno una lunghezza superiore a 255 caratteri, il confronto LIKE sarà basato solo sui primi 255 caratteri.  
  
 Un oggetto LIKE usato in una routine è supportato solo con i modelli costanti. I driver di database desktop supportano SQL-92 come i criteri di ricerca.  
  
 L'uso di una clausola escape in un predicato LIKE non è supportato.  
  
 Un confronto LIKE non deve essere eseguito su una colonna contenente dati di tipo numerico o float. I risultati potrebbero essere imprevedibili. Per ulteriori informazioni, vedere la *Guida per programmatori Microsoft Jet motore di database*.
