---
title: Tipi di dati di campo di Visual FoxPro Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72313e0269c93bca9cb2561d89604c3c88c8567b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304802"
---
# <a name="visual-foxpro-field-data-types"></a>Tipi di dati dei campi Visual FoxPro
Nella tabella seguente sono elencati i valori per l'argomento *FieldType* in ALTER TABLE e CREATE TABLE e viene indicato se sono necessari gli argomenti *nFieldWidth* e *nPrecision.*  
  
|*Fieldtype*|*NFieldWidth (LarghezzaCampo)*|*nPrecisione*|Descrizione|  
|-----------------|-------------------|------------------|-----------------|  
|b|-|d|Double|  
|C|N|-|Campo carattere della larghezza *n*|  
|D|-|-|Data|  
|F|N|d|Campo numerico mobile della larghezza *n* con posizioni decimali *d*|  
|G|-|-|Generale|  
|I|-|-|Integer|  
|L|-|-|Logico|  
|M|-|-|Memo|  
|N|N|d|Campo numerico della larghezza *n* con posizioni decimali *d*|  
|T|-|-|Datetime|  
|S|-|-|Valuta|
