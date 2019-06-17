---
title: Allocato in modo esplicito i descrittori | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fbec69e0d984d843abc2b8754e111a1199c79a5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049790"
---
# <a name="explicitly-allocated-descriptors"></a>Descrittori allocati in modo esplicito
Un'applicazione può allocare in modo esplicito un descrittore applicazione su una connessione in qualsiasi momento che è connesso al database. Specificando l'handle descrittore come un attributo di un'istruzione di gestire tramite **SQLSetStmtAttr**, l'applicazione indirizza il driver da usare quel descrittore al posto di corrispondente allocata in modo implicito dell'applicazione descrittori. L'applicazione non è possibile specificare i descrittori di implementazione alternativa.  
  
 Un'applicazione è possibile associare più di un'istruzione di un descrittore allocato in modo esplicito. Solo quando un'applicazione è effettivamente connesso al database un descrittore può essere un descrittore allocato in modo esplicito. L'applicazione può liberare un descrittore di questo tipo in modo esplicito o implicito liberando la connessione.
