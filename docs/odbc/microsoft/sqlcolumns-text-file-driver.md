---
title: SQLColumns (Driver file di testo) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColumns
- SQLColumns function [ODBC], Text File Driver
ms.assetid: c99e5f8d-4e43-48f8-9e0e-086707b411f5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78c2e20f12dedf399ab36dd908f83aa93bebffc4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307868"
---
# <a name="sqlcolumns-text-file-driver"></a>SQLColumns (driver file di testo)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di file di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Colonna|Commenti|  
|------------|--------------|  
|TABLE_QUALIFIER|Viene restituito il percorso di una directory.|  
|TABLE_OWNER|VIENE restituito NULL in questa colonna perché il nome del proprietario non è supportato.|  
|NULLABLE|SQL_NO_NULLS viene restituito per le colonne che fanno parte di una chiave primaria o di un indice univoco.|
