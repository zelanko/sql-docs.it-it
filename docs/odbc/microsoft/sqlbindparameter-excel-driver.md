---
title: SQLBindParameter (Excel Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLBindParameter
- SQLBindParameter function [ODBC], Excel Driver
ms.assetid: 40489bc5-3e2a-425e-892d-e0dc037f4d7a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84f6e44f4849db81c591a791674878190f21e486
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298043"
---
# <a name="sqlbindparameter-excel-driver"></a>SQLBindParameter (driver Excel)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver Excel. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando viene usato il driver di Microsoft Excel, l'esecuzione di un'istruzione INSERT che usa un parametro per inserire un valore NULL in una colonna SQL_CHAR restituirà SQL_SUCCESS_WITH_INFO, con SQLSTATE 01004, "Dati troncati".
