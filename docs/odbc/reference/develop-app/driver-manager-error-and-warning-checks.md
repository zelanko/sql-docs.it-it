---
title: Controlli di errore e di avviso di gestione driver | Microsoft Docs
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
ms.openlocfilehash: 6d0b136b9748de1991888abb0c19bc0d2ac65ea0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046974"
---
# <a name="driver-manager-error-and-warning-checks"></a>Errore di Gestione driver e controlli di avviso
Gestione driver implementa completamente o parzialmente una serie di funzioni, quindi controlla tutti gli errori e gli avvisi presenti in tali funzioni.  
  
-   Gestione driver implementa **SQLDataSources** e **SQLDrivers** e controlla tutti gli errori e gli avvisi in queste funzioni.  
  
-   Gestione driver controlla se un driver implementa **SQLGetFunctions**. Se il driver non implementa **SQLGetFunctions**, gestione driver implementa e controlla tutti gli errori e gli avvisi al suo interno.  
  
-   Gestione driver implementa parzialmente **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**, **SQLFreeHandle**, **SQLGetDiagRec**e **SQLGetDiagField** e verifica la presenza di alcuni errori in queste funzioni. Può restituire gli stessi errori del driver per alcune di queste funzioni perché entrambe eseguono operazioni simili. È ad esempio possibile che il driver o la gestione driver restituisca SQLSTATE IM008 (Dialog failed) se uno dei due non è in grado di visualizzare una finestra di dialogo di accesso per **SQLDriverConnect**.
