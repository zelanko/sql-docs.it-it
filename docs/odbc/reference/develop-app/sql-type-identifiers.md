---
title: Identificatori di tipo SQL Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 95bf46844e9ed91aac1ec6cb93a298995f0901d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299771"
---
# <a name="sql-type-identifiers"></a>Identificatori dei tipi SQL
Ogni origine dati definisce i propri tipi di dati SQL. ODBC definisce gli identificatori di tipo e descrive le caratteristiche generali dei tipi di dati SQL di cui è possibile eseguire il mapping a ogni identificatore di tipo. È specifico del driver come ogni tipo di dati nell'origine dati sottostante viene mappato a un identificatore di tipo SQL di ODBC.  
  
 Ad esempio, SQL_CHAR è l'identificatore di tipo per una colonna di caratteri con una lunghezza fissa, in genere tra 1 e 254 caratteri. Queste caratteristiche corrispondono al tipo di dati CHAR disponibile in molte origini dati SQL. Pertanto, quando un'applicazione rileva che l'identificatore di tipo per una colonna è SQL_CHAR, si può supporre che è probabilmente avere a che fare con una colonna CHAR. Tuttavia, deve comunque controllare la lunghezza in byte della colonna prima di presumere che sia compresa tra 1 e 254 caratteri; il driver per un'origine dati non SQL, ad esempio, potrebbe eseguire il mapping di una colonna di caratteri a lunghezza fissa di 500 caratteri a SQL_CHAR o SQL_LONGVARCHAR, poiché non esiste una corrispondenza esatta.  
  
 ODBC definisce un'ampia gamma di identificatori di tipo SQL. Tuttavia, il driver non è necessario utilizzare tutti questi identificatori. Al contrario, utilizza solo gli identificatori necessari per esporre i tipi di dati SQL supportati dall'origine dati sottostante. Se l'origine dati sottostante supporta i tipi di dati SQL a cui non corrisponde alcun identificatore di tipo, il driver può definire identificatori di tipo aggiuntivi. Per ulteriori informazioni, vedere [Tipi di dati specifici del driver, Tipi di descrittore, Tipi di informazioni, Tipi di diagnostica e Attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Per una descrizione completa degli identificatori di tipo SQL, vedere [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) nell'Appendice D: tipi di dati.
