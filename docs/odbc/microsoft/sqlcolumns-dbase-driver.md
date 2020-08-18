---
description: SQLColumns (driver dBASE)
title: SQLColumns (driver dBASE) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4998c6a3105add42a874a3fe295960be6dec270
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412077"
---
# <a name="sqlcolumns-dbase-driver"></a>SQLColumns (driver dBASE)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver dBASE. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Colonna|Commenti|  
|------------|--------------|  
|TABLE_QUALIFIER|Viene restituito il percorso di una directory.|  
|TABLE_OWNER|In questa colonna viene restituito NULL perché il nome del proprietario non è supportato.|  
|NULLABLE|Viene restituito SQL_NO_NULLS per le colonne che fanno parte di una chiave primaria o di un indice univoco.|
