---
title: Segnalibri di lunghezza fissa | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e40947dc4dbad0830444870ea7e2d0c663490b25
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188964"
---
# <a name="fixed-length-bookmarks"></a>Segnalibri di lunghezza fissa
Se un'applicazione ODBC 3 *. x* driver dovrebbero funzionare con un'API ODBC 2. *x* dell'applicazione che utilizza segnalibri di lunghezza fissa, il driver devono supportare quanto segue:  
  
-   SQL_UB_ON come valore per l'opzione dell'istruzione SQL_USE_BOOKMARKS. (Deprecata in ODBC 3 SQL_UB_ON*x*.)  
  
-   L'opzione dell'istruzione SQL_GET_BOOKMARK.
