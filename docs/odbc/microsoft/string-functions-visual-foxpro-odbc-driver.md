---
title: Funzioni di stringa (driver ODBC di Visual FoxPro) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 988ba23b95f6b138148b1fa17ad303d7aa2dc895
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299191"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>Funzioni per i valori stringa (driver ODBC Visual FoxPro)
Nella tabella seguente sono elencate le funzioni di modifica delle stringhe ODBC supportate dal driver ODBC di Visual FoxPro. Quando la grammatica di Visual FoxPro per la stessa funzione è diversa dalla sintassi ODBC, viene elencato l'equivalente di Visual FoxPro.  
  
|Grammatica ODBC|Grammatica di Visual FoxPro|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *(codice)*|CHR *(string_exp)*|  
|CONCAT *(string_exp1, string_exp2)*|*string_exp1 - string_exp2*|  
|DIFFERENZA *(string_exp1, string_exp2)*||  
|INSERT *(string_exp1, inizio, lunghezza, string_exp2)*|STUFF *(string_exp1, inizio, lunghezza, string_exp2)*|  
|LCASE *(string_exp)*|LOWER *(string_exp)*|  
|SINISTRA *(string_exp, conteggio)*||  
|LENGTH *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|REPEAT *(string_exp, conteggio)*|REPLICATE *(string_exp, conteggio)*|  
|REPLACE *(string_exp1, string_exp2, string_exp3)*|STRTRAN *(string_exp1, string_exp2, string_exp3)*|  
|DESTRA *(string_exp, conteggio)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|SPACE *(conteggio)*||  
|SOTTOstringa *(string_exp, inizio, lunghezza)*|SUBSTR *(string_exp, inizio, lunghezza)*|  
|UCASE *(string_exp)*|SUPERIORE *(string_exp)*|
