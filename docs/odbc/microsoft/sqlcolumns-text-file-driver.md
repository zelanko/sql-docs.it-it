---
title: SQLColumns (Driver File di testo) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8189a5f6a89f072988404e722a88c29af2d88ca6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62665795"
---
# <a name="sqlcolumns-text-file-driver"></a>SQLColumns (driver file di testo)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver File di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|colonna|Commenti|  
|------------|--------------|  
|TABLE_QUALIFIER|Viene restituito il percorso di una directory.|  
|TABLE_OWNER|Poiché il nome del proprietario non è supportato in questa colonna viene restituito NULL.|  
|NULLABLE|SQL_NO_NULLS viene restituito per le colonne che fanno parte di una chiave primaria o un indice univoco.|
