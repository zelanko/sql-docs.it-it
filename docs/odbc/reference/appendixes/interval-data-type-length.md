---
title: Lunghezza del tipo di dati interval | Microsoft Docs
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
ms.openlocfilehash: a456db12ddb2594dc7b4c9e4f5c26e9cb4245621
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947589"
---
# <a name="interval-data-type-length"></a>Lunghezza del tipo di dati intervallo
Le regole seguenti vengono utilizzate per determinare la lunghezza di un tipo di dati intervallo in caratteri. La lunghezza è espressa in numero di caratteri. Il numero di byte dipende dal set di caratteri. La lunghezza include i valori seguenti aggiunti insieme:  
  
-   Due caratteri per ogni campo nell'intervallo che non è il campo iniziali.  
  
-   Per il campo principale, il numero di caratteri che rappresenta la precisione leader espressa o implicita. Se la precisione principale non è specificata, il valore predefinito è 2.  
  
-   Un carattere per il separatore tra i campi.  
  
-   Uno più la precisione espressa o implicita in secondi. Se la precisione dei secondi non è specificata, il valore predefinito è 6.  
  
 I valori di lunghezza di colonna specifici per ogni tipo di dati intervallo sono contenuti nelle [dimensioni della colonna](../../../odbc/reference/appendixes/column-size.md).
