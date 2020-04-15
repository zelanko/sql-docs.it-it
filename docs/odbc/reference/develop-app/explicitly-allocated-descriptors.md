---
title: Descrittori allocati in modo esplicito Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9950bc23a1e75606316039e6c2d66f3dba59940
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305692"
---
# <a name="explicitly-allocated-descriptors"></a>Descrittori allocati in modo esplicito
Un'applicazione può allocare in modo esplicito un descrittore dell'applicazione su una connessione ogni volta che è connesso al database. Specificando tale handle del descrittore come attributo di un handle di istruzione mediante **SQLSetStmtAttr**, l'applicazione indica al driver di utilizzare tale descrittore al posto dei descrittori di applicazione allocati in modo implicito corrispondenti. L'applicazione non può specificare descrittori di implementazione alternativi.  
  
 Un'applicazione può associare un descrittore allocato in modo esplicito a più di un'istruzione. Solo quando un'applicazione è effettivamente connessa al database può un descrittore essere un descrittore allocato in modo esplicito. L'applicazione può liberare tale descrittore in modo esplicito o implicito liberando la connessione.
