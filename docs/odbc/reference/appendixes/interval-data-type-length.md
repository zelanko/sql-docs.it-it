---
title: Lunghezza del tipo di dati Interval | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- length of data types [ODBC]
- interval data type [ODBC], length
ms.assetid: e9eb38d8-f9db-4401-8c62-aa394054cbbf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16d0590d3297b52891bf399822ce984674022583
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188914"
---
# <a name="interval-data-type-length"></a>Lunghezza del tipo di dati intervallo
Le regole seguenti vengono utilizzate per determinare la lunghezza di un tipo di dati di intervallo in caratteri. Lunghezza è espressa in numero di caratteri. Il numero di byte varia a seconda del set di caratteri. La lunghezza include i seguenti valori sommati:  
  
-   Due caratteri per ogni campo nell'intervallo che non corrisponde al campo iniziale.  
  
-   Per il campo iniziale, il numero di caratteri che rappresenta la precisione iniziale espressa o implicita. Se la precisione iniziale non è specificata, il valore predefinito è 2.  
  
-   Un singolo carattere per il separatore tra i campi.  
  
-   Uno oltre la precisione dei secondi espressa o implicita. Se la precisione dei secondi non è specificata, il valore predefinito è 6.  
  
 I valori di lunghezza di colonna specifici per ogni tipo di dati di intervallo sono contenuti nel [le dimensioni di colonna](../../../odbc/reference/appendixes/column-size.md).
