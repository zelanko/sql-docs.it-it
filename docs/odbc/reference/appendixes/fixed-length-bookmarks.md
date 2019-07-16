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
ms.openlocfilehash: 5877a6cb7a99803f854338321e333c87037c2e90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913580"
---
# <a name="fixed-length-bookmarks"></a>Segnalibri di lunghezza fissa
Se un database ODBC *3.x* driver dovrebbero funzionare con un database ODBC *2.x* dell'applicazione che utilizza segnalibri di lunghezza fissa, il driver devono supportare quanto segue:  
  
-   SQL_UB_ON come valore per l'opzione dell'istruzione SQL_USE_BOOKMARKS. (SQL_UB_ON è deprecato in ODBC *3.x*.)  
  
-   L'opzione dell'istruzione SQL_GET_BOOKMARK.
