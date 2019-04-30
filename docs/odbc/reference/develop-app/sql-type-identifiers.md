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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1763ee0cd8c5bc2017160de44b9c047781649eba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150028"
---
# <a name="sql-type-identifiers"></a>Identificatori dei tipi SQL
Ogni origine dati definisce i propri tipi di dati SQL. ODBC definisce gli identificatori di tipo e vengono descritte le caratteristiche generali dei tipi di dati SQL che potrebbero essere mappati a ogni identificatore di tipo. È come ogni tipo di dati nell'origine dati sottostante viene eseguito il mapping a un identificatore di tipo SQL ODBC specifiche del driver.  
  
 Ad esempio SQL_CHAR è l'identificatore di tipo per una colonna di tipo carattere a lunghezza fissa, in genere compreso tra 1 e 254 caratteri. Queste caratteristiche corrispondono al tipo di dati CHAR disponibile in molte origini dati SQL. Di conseguenza, quando un'applicazione rileva che l'identificatore del tipo per una colonna è SQL_CHAR, può presupporre che probabilmente interagendo con una colonna CHAR. Tuttavia, è necessario verificare sempre la lunghezza in byte della colonna prima di presumere che si è compreso tra 1 e 254 caratteri. il driver per un'origine dati non SQL, ad esempio, potrebbe eseguire il mapping di una colonna di tipo carattere a lunghezza fissa di 500 caratteri SQL_CHAR o SQL_LONGVARCHAR, perché nessuno dei due sia una corrispondenza esatta.  
  
 ODBC definisce un'ampia gamma di identificatori di tipo SQL. Tuttavia, il driver non è necessario usare tutti questi identificatori. Usa invece solo tali identificatori che deve esporre tipi di dati SQL supportati dall'origine dati sottostante. Se l'origine dati sottostante supporta i tipi di dati SQL per cui alcun identificatore di tipo non corrispondente, il driver può definire gli identificatori di tipo aggiuntivi. Per altre informazioni, vedere [tipi di dati specifici del Driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e gli attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Per una descrizione completa degli identificatori di tipo SQL, vedere [tipi di dati C](../../../odbc/reference/appendixes/c-data-types.md) nell'appendice d: Tipi di dati.
