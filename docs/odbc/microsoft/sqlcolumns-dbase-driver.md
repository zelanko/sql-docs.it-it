---
title: SQLColumns (Driver dBASE) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLColumns
ms.assetid: 168171de-ab7d-4b5b-af7f-6e2106adfcce
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3a3227556a3adfe63431f0cf10169a29d434495
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62666131"
---
# <a name="sqlcolumns-dbase-driver"></a>SQLColumns (driver dBASE)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver dBASE. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|colonna|Commenti|  
|------------|--------------|  
|TABLE_QUALIFIER|Viene restituito il percorso di una directory.|  
|TABLE_OWNER|Poiché il nome del proprietario non è supportato in questa colonna viene restituito NULL.|  
|NULLABLE|SQL_NO_NULLS viene restituito per le colonne che fanno parte di una chiave primaria o un indice univoco.|
