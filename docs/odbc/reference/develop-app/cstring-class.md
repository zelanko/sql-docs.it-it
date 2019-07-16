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
ms.openlocfilehash: 90c92476337bb1059b7272830e33094edc58dbd9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002077"
---
# <a name="cstring-class"></a>Classe CString
Poiché gli oggetti del **CString** classe in Microsoft® Visual C++® sono firmati e gli argomenti delle stringhe in funzioni di ODBC non sono firmati, le applicazioni che passano **CString** oggetti alle funzioni ODBC senza esegue il cast di essi riceverà gli avvisi del compilatore.
