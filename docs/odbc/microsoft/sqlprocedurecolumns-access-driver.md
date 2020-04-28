---
title: SQLProcedureColumns (driver Access) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be17776ac6b6879140a7c57bede1b3cb539d97be
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299461"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di accesso. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Gli sviluppatori di applicazioni devono cercare le colonne definite dal driver a partire dalla fine del set di risultati e procedere all'indietro.  
  
|Colonna|Commenti|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT o SQL_RESULT_COL|  
|ORDINALE|Si tratta di una colonna specifica del driver restituita alla fine del set di risultati. Il tipo SQL della colonna è un numero intero.|
