---
title: Errore di Gestione driver e controlli di avviso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e00b6907d58cda1708cf61907d3c5ff6bf56edfa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238039"
---
# <a name="driver-manager-error-and-warning-checks"></a>Errore di Gestione driver e controlli di avviso
Gestione Driver completamente o parzialmente implementa una serie di funzioni e quindi verifica la presenza di tutti o alcuni degli errori e avvisi in tali funzioni.  
  
-   Implementa gestione Driver **SQLDataSources** e **SQLDrivers** e verifica se tutti gli errori e avvisi in queste funzioni.  
  
-   Gestione Driver verifica se un driver implementa **SQLGetFunctions**. Se il driver non implementa **SQLGetFunctions**, gestione Driver implementa e verifica la presenza di tutti gli errori e avvisi in esso.  
  
-   Gestione Driver implementa parzialmente **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**,  **SQLFreeHandle**, **SQLGetDiagRec**, e **SQLGetDiagField** e verifiche per alcuni errori in queste funzioni. Può restituire gli stessi errori come il driver per alcune di queste funzioni perché entrambi eseguono operazioni simili. Ad esempio, il Driver Manager o il driver può restituire SQLSTATE IM008 (finestra di dialogo non riuscita) se uno è in grado di visualizzare una finestra di dialogo account di accesso per **SQLDriverConnect**.
