---
title: HStmt multipli (Driver Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple hstmts [ODBC]
- Paradox driver [ODBC], multiple hstmts
ms.assetid: 66aecd94-092d-43d4-9583-74f5e2990eac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5e7a9a4ec0d6426779fb55d923bc7f0607089aad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045035"
---
# <a name="multiple-hstmts-paradox-driver"></a>hstmt multipli (driver Paradox)
Quando viene utilizzato il driver ODBC Paradox, se si desidera utilizzare più di uno *hstmt* per eseguire query su una tabella, la tabella deve avere un indice univoco (chiave primaria Paradox).
