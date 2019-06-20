---
title: Tipi di segnalibro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f5c5a126ea220f055349ad00dc950281606ed4c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199248"
---
# <a name="bookmark-types"></a>Tipi di segnalibro
Tutti i segnalibri in ODBC 3*x* sono a lunghezza variabile segnalibri. In questo modo una chiave primaria o un indice univoco associato a una tabella da usare come segnalibro. Il segnalibro inoltre può essere un valore a 32 bit, come è stato usato in ODBC 2. *x*. Per specificare che un segnalibro viene utilizzato con un cursore, un'applicazione ODBC 3*x* applicazione imposta l'attributo di istruzione SQL_ATTR_USE_BOOKMARK SQL_UB_VARIABLE. Viene utilizzato automaticamente un segnalibro a lunghezza variabile.  
  
 Un'applicazione può chiamare **SQLColAttribute** con il *FieldIdentifier* argomento impostato su SQL_DESC_OCTET_LENGTH per ottenere la lunghezza del segnalibro. Poiché un segnalibro a lunghezza variabile può essere un valore long, un'applicazione non deve essere associato alla colonna 0, a meno che userà il segnalibro per numero di righe nel set di righe.  
  
 Segnalibri di lunghezza fissa sono supportati solo per compatibilità con le versioni precedenti. Se un ODBC 2. *x* funziona con un'applicazione ODBC 3 *. x* driver chiama **SQLSetStmtOption** per impostare SQL_USE_BOOKMARKS SQL_UB_ON, questo viene mappato a SQL_UB_VARIABLE in Gestione Driver . Viene utilizzato un segnalibro a lunghezza variabile, anche se vengono popolate solo 32 bit di esso. Se un driver supporta segnalibri di lunghezza fissa, supporterà a lunghezza variabile segnalibri. Se un'applicazione ODBC 3 *. x* funziona con un'API ODBC 2. *x* driver chiama **SQLSetStmtAttr** per impostare SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE, questo viene mappato a SQL_UB_ON in Gestione Driver e viene utilizzato un segnalibro a lunghezza fissa a 32 bit. L'attributo di istruzione SQL_ATTR_FETCH_BOOKMARK_PTR quindi deve puntare a un segnalibro a 32 bit. Se i segnalibri usati sono più di 32 bit, ad esempio quando le chiavi primarie vengono utilizzate come segnalibri, il cursore deve eseguire il mapping ai valori effettivi a valori a 32 bit. Ad esempio, possibile, creare una tabella hash di essi. Quando un'applicazione ODBC 3 *. x* funziona con un'API ODBC 2. *x* driver associa un segnalibro, la lunghezza del buffer deve essere 4.
