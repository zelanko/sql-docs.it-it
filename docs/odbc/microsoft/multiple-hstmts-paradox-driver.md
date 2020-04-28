---
title: Più hstmt (driver Paradox) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac381024a6b4b67719cb7c098367f63a6176bad0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298191"
---
# <a name="multiple-hstmts-paradox-driver"></a>hstmt multipli (driver Paradox)
Quando si utilizza il driver ODBC Paradox, se si desidera utilizzare più di un *HSTMT* per eseguire query su una tabella, è necessario che la tabella disponga di un indice univoco (chiave primaria Paradox).
