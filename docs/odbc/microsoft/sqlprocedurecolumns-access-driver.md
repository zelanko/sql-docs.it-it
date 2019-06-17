---
title: SQLProcedureColumns (Driver Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a438823d1aa71eecb25c4935026c1b43e45842d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62637387"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni di accesso specifici del Driver. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Gli sviluppatori di applicazioni devono cercare di colonne definite dal driver di avvio alla fine del set di risultati e andando a ritroso.  
  
|colonna|Commenti|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT or SQL_RESULT_COL|  
|NUMERO ORDINALE|Si tratta di una colonna specifici del driver che viene restituita alla fine del set di risultati. Il tipo SQL della colonna è un numero intero.|
