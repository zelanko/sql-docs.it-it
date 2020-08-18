---
description: SQLColAttributes (driver file di testo)
title: SQLColAttributes (driver file di testo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], Text File Driver
ms.assetid: 132fd1c0-1921-4a7d-910e-aedf1bff5453
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee659f984f75b3ede7fc09e698e58b427158f9fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412207"
---
# <a name="sqlcolattributes-text-file-driver"></a>SQLColAttributes (driver file di testo)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver del file di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Attributo|Commenti|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Per i dati di LONGVARBINARY, SQL_COLUMN_DISPLAY_SIZE è la lunghezza massima della colonna, non la lunghezza massima della colonna per 2.|  
|SQL_OWNER_NAME|In questa colonna viene restituita una stringa vuota ("") perché il nome del proprietario non è supportato.|  
|SQL_QUALIFIER_NAME|Viene restituito il percorso di una directory.|  
|SQL_COLUMN_SEARCHABLE|Le colonne LONGVARBINARY e LONGVARCHAR sono segnalate come SQL_UNSEARCHABLE.<br /><br /> I tipi di dati binary e character a lunghezza fissa e a lunghezza variabile sono disponibili per la ricerca, anche se LONGVARBINARY e LONGVARCHAR non lo sono.|
