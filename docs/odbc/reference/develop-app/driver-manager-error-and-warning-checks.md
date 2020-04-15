---
title: Controlli di errore e di avviso di Gestione driver Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee8a0f5ebfac8b6f87281806f07989f4980eb9b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305783"
---
# <a name="driver-manager-error-and-warning-checks"></a>Errore di Gestione driver e controlli di avviso
Gestione Driver implementa completamente o parzialmente una serie di funzioni e pertanto controlla tutti o alcuni degli errori e degli avvisi in tali funzioni.  
  
-   Gestione Driver implementa **SQLDataSources** e **SQLDrivers** e controlla tutti gli errori e gli avvisi in queste funzioni.  
  
-   Gestione Driver controlla se un driver implementa **SQLGetFunctions**. Se il driver non implementa **SQLGetFunctions**, Gestione Driver implementa e verifica la presenza di tutti gli errori e gli avvisi in esso in esso.  
  
-   Gestione Driver implementa parzialmente **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**, **SQLFreeHandle**, **SQLGetDiagRec**e **SQLGetDiagField** e verifica la presenza di alcuni errori in queste funzioni. Può restituire gli stessi errori del driver per alcune di queste funzioni perché entrambe eseguono operazioni simili. Ad esempio, Gestione Driver o driver può restituire SQLSTATE IM008 (finestra di dialogo non riuscita) se uno dei due non è in grado di visualizzare una finestra di dialogo di accesso per **SQLDriverConnect**.
