---
title: Classe CString | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CString class [ODBC]
ms.assetid: 18630642-76fa-43c4-a154-3f0969ec9b50
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f5752602de4848b35298fb4c4a6a1efdf6519dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042487"
---
# <a name="cstring-class"></a>Classe CString
Poiché gli oggetti del **CString** classe in Microsoft® Visual C++® sono firmati e gli argomenti delle stringhe in funzioni di ODBC non sono firmati, le applicazioni che passano **CString** oggetti alle funzioni ODBC senza esegue il cast di essi riceverà gli avvisi del compilatore.
