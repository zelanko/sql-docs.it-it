---
title: Interval Data Type Length (Lunghezza del tipo di dati Intervallo) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68bb4daa47cb58d5a0ff7b680a2d2154fb14b345
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284321"
---
# <a name="interval-data-type-length"></a>Lunghezza del tipo di dati intervallo
Le regole seguenti vengono utilizzate per determinare la lunghezza di un tipo di dati intervallo in caratteri. La lunghezza è espressa in numero di caratteri. Il numero di byte dipende dal set di caratteri. La lunghezza include i seguenti valori sommati:  
  
-   Due caratteri per ogni campo dell'intervallo che non è il campo iniziale.  
  
-   Per il campo iniziale, il numero di caratteri che è la precisione iniziale o implicita. Se la precisione di interlinea non è specificata, il valore predefinito è 2.If the leading precision is not specified, the default value is 2.  
  
-   Un carattere per il separatore tra i campi.  
  
-   Uno più la precisione espressa o implicita secondi. Se la precisione dei secondi non è specificata, il valore predefinito è 6.  
  
 In [Dimensioni colonna](../../../odbc/reference/appendixes/column-size.md)sono contenuti valori di lunghezza di colonna specifici per ogni tipo di dati intervallo.
