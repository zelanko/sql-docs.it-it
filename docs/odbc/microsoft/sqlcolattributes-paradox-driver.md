---
title: SQLColAttributes (Driver Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLColAttributes
ms.assetid: bbeef024-d470-4d28-b61b-26997ef41007
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 330cdf7a48b17bab5cb912d3a520b8d98635d652
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62666164"
---
# <a name="sqlcolattributes-paradox-driver"></a>SQLColAttributes (driver Paradox)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver Paradox. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|attribute|Commenti|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Per i dati, LONGVARBINARY SQL_COLUMN_DISPLAY_SIZE è la lunghezza massima della colonna, non la lunghezza massima della colonna volte 2.|  
|SQL_OWNER_NAME|Una stringa vuota ("") in questa colonna viene restituito perché il nome del proprietario non è supportato.|  
|SQL_QUALIFIER_NAME|Viene restituito il percorso di una directory.|  
|SQL_COLUMN_SEARCHABLE|Colonne LONGVARCHAR e LONGVARBINARY vengono segnalate come SQL_UNSEARCHABLE.<br /><br /> Tipi di dati carattere e binari a lunghezza fissa e a lunghezza variabile sono ricercabili, anche se non sono LONGVARCHAR e LONGVARBINARY.|  
  
> [!NOTE]  
>  Il codice precedente non è un elenco completo degli attributi restituiti da **SQLColAttributes**.
