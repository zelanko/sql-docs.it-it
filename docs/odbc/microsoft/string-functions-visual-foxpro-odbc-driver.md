---
description: Funzioni per i valori stringa (driver ODBC Visual FoxPro)
title: Funzioni stringa (driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.openlocfilehash: 4ab2ecefb604183b0387a561f72494028c62d15f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471543"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>Funzioni per i valori stringa (driver ODBC Visual FoxPro)
Nella tabella seguente sono elencate le funzioni di modifica delle stringhe ODBC supportate dal driver ODBC Visual FoxPro. Quando la grammatica Visual FoxPro per la stessa funzione differisce dalla sintassi ODBC, viene elencato l'equivalente Visual FoxPro.  
  
|Grammatica ODBC|Grammatica Visual FoxPro|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *(codice)*|CHR *(string_exp)*|  
|CONCAt *(string_exp1, string_exp2)*|*string_exp1 + string_exp2*|  
|DIFFERENZA *(string_exp1, string_exp2)*||  
|Inserisci *(string_exp1, inizio, lunghezza, string_exp2)*|STUFF *(string_exp1, inizio, lunghezza, string_exp2)*|  
|LCASE *(string_exp)*|INFERIORE *(string_exp)*|  
|LEFT *(string_exp, conteggio)*||  
|LUNGHEZZA *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|Ripeti *(string_exp, conteggio)*|REPLICAte *(string_exp, conteggio)*|  
|SOSTITUISCi *(string_exp1, string_exp2, string_exp3)*|STRTRAN *(string_exp1, string_exp2, string_exp3)*|  
|RIGHT *(string_exp, conteggio)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|SPAZIO *(conteggio)*||  
|Substring *(string_exp, inizio, lunghezza)*|SUBSTR *(string_exp, inizio, lunghezza)*|  
|UCASE *(string_exp)*|SUPERIORE *(string_exp)*|
