---
title: SQLColAttributes (Driver di accesso) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Access Driver
- Access driver [ODBC], SQLColAttributes
ms.assetid: adb6f81d-e8c7-4748-9b1d-f7a053788bbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15770ac260ad8ea864dc78bf00c5b9e8bd964dbe
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307962"
---
# <a name="sqlcolattributes-access-driver"></a>SQLColAttributes (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di accesso. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Attributo|Commenti|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Per i dati LONGVARBINARY, SQL_COLUMN_DISPLAY_SIZE è la lunghezza massima della colonna, non la lunghezza massima della colonna per 2.|  
|SQL_OWNER_NAME|In questa colonna viene restituita una stringa vuota ("") perché il nome del proprietario non è supportato.|  
|SQL_QUALIFIER_NAME|Viene restituito il percorso di un file di database.|  
|SQL_COLUMN_SEARCHABLE|Le colonne LONGVARBINARY e LONGVARCHAR vengono segnalate come SQL_UNSEARCHABLE.<br /><br /> I tipi di dati binari e di tipo carattere a lunghezza fissa e variabile sono ricercabili, anche se LONGVARBINARY e LONGVARCHAR non lo sono.|  
  
> [!NOTE]  
>  Quanto sopra non è un elenco completo degli attributi restituiti da **SQLColAttributes**.
