---
title: Identificatori di tipo SQL | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299771"
---
# <a name="sql-type-identifiers"></a>Identificatori dei tipi SQL
Ogni origine dati definisce i propri tipi di dati SQL. ODBC definisce gli identificatori di tipo e descrive le caratteristiche generali dei tipi di dati SQL di cui è possibile eseguire il mapping a ogni identificatore di tipo. Indica il modo in cui ogni tipo di dati nell'origine dati sottostante viene mappato a un identificatore di tipo SQL di ODBC.  
  
 Ad esempio, SQL_CHAR è l'identificatore di tipo per una colonna di tipo carattere con una lunghezza fissa, in genere compresa tra 1 e 254 caratteri. Queste caratteristiche corrispondono al tipo di dati CHAR trovato in molte origini dati SQL. Pertanto, quando un'applicazione rileva che l'identificatore di tipo per una colonna è SQL_CHAR, è possibile che si tratti di una colonna CHAR. Tuttavia, deve comunque controllare la lunghezza in byte della colonna prima di presumere che sia compresa tra 1 e 254 caratteri; il driver per un'origine dati non SQL, ad esempio, può eseguire il mapping di una colonna di tipo carattere a lunghezza fissa di 500 caratteri a SQL_CHAR o SQL_LONGVARCHAR, perché nessuno dei due è una corrispondenza esatta.  
  
 ODBC definisce un'ampia gamma di identificatori di tipo SQL. Tuttavia, non è necessario che il driver usi tutti questi identificatori. USA invece solo gli identificatori necessari per esporre i tipi di dati SQL supportati dall'origine dati sottostante. Se l'origine dati sottostante supporta i tipi di dati SQL a cui non corrisponde alcun identificatore di tipo, il driver può definire identificatori di tipo aggiuntivi. Per ulteriori informazioni, vedere [tipi di dati specifici del driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Per una descrizione completa degli identificatori di tipo SQL, vedere [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) in Appendice D: tipi di dati.
