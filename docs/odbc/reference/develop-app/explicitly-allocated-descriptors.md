---
title: Descrittori allocati in modo esplicito | Microsoft Docs
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
ms.openlocfilehash: 5808265a9ab70b9947cea64fef790497c7229da8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069936"
---
# <a name="explicitly-allocated-descriptors"></a>Descrittori allocati in modo esplicito
Un'applicazione può allocare in modo esplicito un descrittore dell'applicazione in una connessione in qualsiasi momento in cui è connessa al database. Specificando l'handle del descrittore come attributo di un handle di istruzione utilizzando **SQLSetStmtAttr**, l'applicazione indirizza il driver in modo che utilizzi tale descrittore al posto dei corrispondenti descrittori dell'applicazione allocati in modo implicito. L'applicazione non può specificare descrittori di implementazione alternativi.  
  
 Un'applicazione può associare un descrittore allocato in modo esplicito a più di un'istruzione. Solo quando un'applicazione è effettivamente connessa al database può essere un descrittore allocato in modo esplicito. L'applicazione può liberare questo descrittore in modo esplicito o in modo implicito liberando la connessione.
