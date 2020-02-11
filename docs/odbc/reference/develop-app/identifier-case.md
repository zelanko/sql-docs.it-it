---
title: Caso identificatore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70728908f081ab89e08cad1265f04394f29b66ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138969"
---
# <a name="identifier-case"></a>Maiuscole/minuscole per gli identificatori
Nelle istruzioni SQL e negli argomenti della funzione Catalog, gli identificatori e gli identificatori delimitati possono essere o meno con distinzione tra maiuscole e minuscole, che un'applicazione può determinare chiamando **SQLGetInfo** con le opzioni SQL_IDENTIFIER_CASE e SQL_QUOTED_IDENTIFIER_CASE.  
  
 Ognuna di queste opzioni ha quattro possibili valori restituiti: uno indica che l'identificatore o il case identificatore tra virgolette è sensibile e tre indica che non è sensibile. I tre valori che non fanno distinzione tra maiuscole e minuscole descrivono ulteriormente il caso in cui gli identificatori vengono archiviati nel catalogo di sistema. Il modo in cui gli identificatori vengono archiviati nel catalogo di sistema è pertinente solo a scopo di visualizzazione, ad esempio quando un'applicazione Visualizza i risultati di una funzione di catalogo. non modifica la distinzione tra maiuscole e minuscole degli identificatori.
