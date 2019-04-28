---
title: SQLColAttributes (Driver Access) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0fa4de89a1ca617f7955d89e18650b7cf1e0c0c2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62865740"
---
# <a name="sqlcolattributes-access-driver"></a>SQLColAttributes (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni di accesso specifici del Driver. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|attribute|Commenti|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Per i dati, LONGVARBINARY SQL_COLUMN_DISPLAY_SIZE è la lunghezza massima della colonna, non la lunghezza massima della colonna volte 2.|  
|SQL_OWNER_NAME|Una stringa vuota ("") in questa colonna viene restituito perché il nome del proprietario non è supportato.|  
|SQL_QUALIFIER_NAME|Viene restituito il percorso di un file di database.|  
|SQL_COLUMN_SEARCHABLE|Colonne LONGVARCHAR e LONGVARBINARY vengono segnalate come SQL_UNSEARCHABLE.<br /><br /> Tipi di dati carattere e binari a lunghezza fissa e a lunghezza variabile sono ricercabili, anche se non sono LONGVARCHAR e LONGVARBINARY.|  
  
> [!NOTE]  
>  Il codice precedente non è un elenco completo degli attributi restituiti da **SQLColAttributes**.
