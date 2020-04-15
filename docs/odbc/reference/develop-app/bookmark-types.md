---
title: Tipi di segnalibri - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26d0297cd9dc57e9f30945a9248b235ae469da3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306332"
---
# <a name="bookmark-types"></a>Tipi di segnalibro
Tutti i segnalibri in ODBC *3.x* sono segnalibri di lunghezza variabile. Ciò consente di utilizzare una chiave primaria o un indice univoco associato a una tabella come segnalibro. Il segnalibro può anche essere un valore a 32 bit, come è stato utilizzato in ODBC *2.x*. Per specificare che un segnalibro viene utilizzato con un cursore, un'applicazione ODBC *3.x* imposta l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARK su SQL_UB_VARIABLE. Viene utilizzato automaticamente un segnalibro di lunghezza variabile.  
  
 Un'applicazione può chiamare **SQLColAttribute** con il *FieldIdentifier* argomento impostato su SQL_DESC_OCTET_LENGTH per ottenere la lunghezza del segnalibro. Poiché un segnalibro di lunghezza variabile può essere un valore long, un'applicazione non deve essere associata alla colonna 0 a meno che non utilizzerà il segnalibro per molte delle righe nel set di righe.  
  
 I segnalibri a lunghezza fissa sono supportati solo per la compatibilità con le versioni precedenti. Se un'applicazione ODBC *2.x* che utilizza un driver ODBC *3.x* chiama **SQLSetStmtOption** per impostare SQL_USE_BOOKMARKS su SQL_UB_ON, viene mappata in Gestione Driver a SQL_UB_VARIABLE. Viene utilizzato un segnalibro di lunghezza variabile, anche se vengono popolati solo 32 bit. Se un driver supporta segnalibri a lunghezza fissa, supporterà segnalibri a lunghezza variabile. Se un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* chiama **SQLSetStmtAttr** per impostare SQL_ATTR_USE_BOOKMARKS su SQL_UB_VARIABLE, viene mappata in Gestione Driver a SQL_UB_ON e viene utilizzato un segnalibro a lunghezza fissa a 32 bit. L'attributo di istruzione SQL_ATTR_FETCH_BOOKMARK_PTR deve quindi puntare a un segnalibro a 32 bit. Se i segnalibri utilizzati sono più lunghi di 32 bit, ad esempio quando le chiavi primarie vengono utilizzate come segnalibri, il cursore deve eseguire il mapping dei valori effettivi a valori a 32 bit. Potrebbe, ad esempio, compilare una tabella hash di loro. Quando un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* associa un segnalibro, la lunghezza del buffer deve essere 4.
