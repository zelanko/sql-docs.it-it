---
title: Chiamata a SQLCloseCursor . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2feab58de28e39747a1d9c819f9f15426b156151
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306274"
---
# <a name="calling-sqlclosecursor"></a>Chiamata di SQLCloseCursor
Poiché **SQLCloseCursor** è quasi uguale a **SQLFreeStmt** con SQL_CLOSE, Gestione Driver non esegue il mapping di questa funzione. Le funzioni di sostituzione vengono mappate in modo che le applicazioni ODBC *2.x* esistenti possano facilmente passare a ODBC *3.x* utilizzando le nuove funzioni. Tale spostamento rende più semplice per tali applicazioni iniziare a utilizzare la nuova funzionalità ODBC *3.x* all'interno del codice condizionale in modo modulare. **SQLCloseCursor** non rappresenta alcuna nuova funzionalità. Un'applicazione non ottiene alcun vantaggio passando a **SQLCloseCursor** da **SQLFreeStmt** con SQL_CLOSE.
