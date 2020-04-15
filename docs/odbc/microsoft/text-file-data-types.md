---
title: Tipi di dati dei file di testo - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7864dc81eaa3dd37f3d0053b2329c8842e445c8d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302659"
---
# <a name="text-file-data-types"></a>Tipi di dati file di testo
Nella tabella seguente viene illustrato il mapping dei tipi di dati di testo ai tipi di dati SQL ODBC. Si noti che non tutti i tipi di dati SQL ODBC sono supportati dal driver di testo ODBC.  
  
|Tipo di dati Testo|Tipo di dati ODBC|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** restituisce i tipi di dati ODBC. Tutte le conversioni nell'Appendice D di *ODBC Programmer's Reference* sono supportate per i tipi di dati SQL elencati nella tabella precedente.  
  
 Nella tabella seguente vengono illustrate le limitazioni relative ai tipi di dati Testo.The following table shows limitations on Text data types.  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|CHAR|La creazione di una colonna CHAR di lunghezza zero o non specificata restituisce in realtà una colonna a 255 bit.<br /><br /> Nei file delimitati, una colonna CHAR può avere o meno delimitatori tra virgolette doppie all'inizio e alla fine; nei file a lunghezza fissa, le virgolette doppie non vengono utilizzate come delimitatori.|  
|DATETIME|MM-GG-AA (ad esempio, 01-17-92)<br /><br /> MMM-GG-AA (ad esempio, gennaio-17-92)<br /><br /> DD-MMM-AA (ad esempio, 17-gen-92)<br /><br /> AAAA-MM-GG (ad esempio, 1992-01-17)<br /><br /> AAAA-MMM-GG (ad esempio, 1992-gen-17)<br /><br /> I separatori di data misti non sono consentiti all'interno di una tabella.<br /><br /> Il formato ISAM di testo formatta un campo DATETIME negli Stati Uniti o in formato europeo, a seconda dell'impostazione internazionale nel Pannello di controllo di Windows.|  
|FLOAT|La larghezza massima include il segno e il separatore decimale. In Schema.ini, la larghezza è indicata come segue:<br /><br /> 14.083 è FLOAT Larghezza 6<br /><br /> -14.083 è FLOAT Larghezza 7<br /><br /> 14.083 USD è FLOAT Larghezza 7<br /><br /> 14083. è FLOAT Larghezza 6<br /><br /> ODBC restituisce sempre 8 per le colonne FLOAT.<br /><br /> Le colonne FLOAT possono anche essere in notazione scientifica, ad esempio:<br /><br /> -3.04E:2 è float Width 8<br /><br /> 25E4 è Float Width 4<br /><br /> **Nota:** La notazione decimale e scientifica non può essere mismitata in una colonna.<br /><br /> I valori NULL sono rappresentati da una stringa vuota con spaziatura in file a lunghezza fissa e vengono omessi nei file delimitati.<br /><br /> I dati mobili possono essere riempiti con spazi vuoti iniziali.|  
|INTEGER|I valori validi per le colonne INTEGER sono compresi tra 32767 e -32766.<br /><br /> In Schema.ini, la larghezza è indicata come segue:<br /><br /> 14083 è INTEGER Larghezza 5<br /><br /> 0 è INTEGER Larghezza 1<br /><br /> ODBC restituisce sempre 4 per le colonne INTEGER.<br /><br /> La larghezza massima include un segno. La larghezza massima di una colonna INTEGER è 11, anche se la larghezza può essere maggiore a causa degli spazi vuoti consentiti nelle tabelle in formato fisso.|  
|LONGCHAR|Il limite teorico sulla larghezza di una colonna LONGCHAR in una tabella a lunghezza fissa o delimitata è 65500K. È più probabile che l'ISAM di testo fornisca un supporto affidabile fino a circa 32K.|  
  
 Ulteriori limitazioni sui tipi di dati sono disponibili in [Limitazioni dei tipi](../../odbc/microsoft/data-type-limitations.md)di dati .
