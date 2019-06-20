---
title: Tipi di dati di File di testo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23416cb067507d821701e57255fdc6f81ee607c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633006"
---
# <a name="text-file-data-types"></a>Tipi di dati file di testo
Nella tabella seguente viene illustrato come tipi di dati di testo vengono eseguito il mapping ai tipi di dati SQL ODBC. Si noti che non tutti i tipi di dati SQL ODBC sono supportati dal driver ODBC testo.  
  
|Tipo di dati text|Tipo di dati ODBC|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** restituisce tipi di dati ODBC. Tutte le conversioni nell'appendice D i *riferimento per programmatori ODBC* sono supportati per i tipi di dati SQL elencati nella tabella precedente.  
  
 La tabella seguente illustra le limitazioni sui tipi di dati di testo.  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|CHAR|Creazione di una colonna CHAR pari a zero o di lunghezza non specificata restituisce effettivamente una colonna bit 255.<br /><br /> Nel file delimitati, una colonna CHAR può o non abbia i delimitatori di virgoletta doppia all'inizio e alla fine; nei file di lunghezza fissa, racchiusi tra virgolette doppie non vengono utilizzati come delimitatori.|  
|DATETIME|MM-DD-YY (ad esempio, 17-01-92)<br /><br /> MMM-DD-YY (ad esempio Gen-17-92)<br /><br /> GG-MMM-AA (ad esempio, 17-Gen-92)<br /><br /> AAAA-MM-GG (ad esempio, 1992-01-17)<br /><br /> AAAA-MMM-GG (ad esempio, 1992-gen-17)<br /><br /> I separatori di data misti non sono consentiti all'interno di una tabella.<br /><br /> ISAM il testo formatta un campo Data/ora nel formato Stati Uniti o in Europa, a seconda dell'impostazione internazionale nel Pannello di controllo di Windows.|  
|FLOAT|La larghezza massima include il segno e un separatore decimale. In schema. ini, la larghezza viene indicata come indicato di seguito:<br /><br /> 14.083 è FLOAT larghezza 6<br /><br /> -14.083 è FLOAT larghezza 7<br /><br /> +14.083 è FLOAT larghezza 7<br /><br /> 14083. è FLOAT larghezza 6<br /><br /> ODBC restituisce sempre 8 per le colonne FLOAT.<br /><br /> FLOAT colonne possono essere anche in notazione scientifica, ad esempio:<br /><br /> -3.04E + 2 è Float larghezza 8<br /><br /> 25E4 è Float larghezza 4<br /><br /> **Nota** notazione scientifica e decimale non può essere combinata in una colonna.<br /><br /> I valori NULL sono rappresentati da una stringa vuota aggiunta nei file di lunghezza fissa e sono stati omessi nei file delimitato da virgole.<br /><br /> Dati float possono essere applicato un riempimento con spazi vuoti iniziali.|  
|INTEGER|I valori validi per le colonne INTEGER sono 32767 per -32766.<br /><br /> In schema. ini, la larghezza viene indicata come indicato di seguito:<br /><br /> 14083 è INTEGER larghezza 5<br /><br /> 0 è 1 la larghezza di INTEGER<br /><br /> ODBC restituisce sempre 4 per colonne di tipo INTEGER.<br /><br /> La larghezza massima include un segno. La larghezza massima di una colonna INTEGER è 11, anche se la larghezza può essere superiore a causa di spazi vuoti che sono consentiti nelle tabelle in formato fisso.|  
|LONGCHAR|Limita la teoria sulla larghezza di una colonna LONGCHAR in uno a lunghezza fissa o tabella delimitato da virgole è 65500K. ISAM il testo è più probabile fornire un supporto affidabile fino a circa 32 KB.|  
  
 Altre limitazioni sui tipi di dati sono disponibili nel [limitazioni del tipo di dati](../../odbc/microsoft/data-type-limitations.md).
