---
title: Supporto di valori null e confronti di logica a tre valori | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4f1b4823db4ae961024ac2a786c948d8349f31be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919628"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Supporto dei valori Null e confronti di logica a tre valori
  Se si ha familiarità con i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile notare la somiglianza nella semantica e nella precisione dello spazio dei nomi `System.Data.SqlTypes` in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Esistono tuttavia alcune differenze, le più importanti delle quali sono illustrate nel presente argomento.  
  
## <a name="null-values"></a>Valori NULL  
 Una differenza importante tra i tipi di dati Common Language Runtime (CLR) nativi e i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste nel fatto che i primi non consentono valori NULL, mentre i secondi forniscono semantica NULL completa.  
  
 La presenza di valori NULL influisce sui confronti. Quando si confrontano due valori x e y, se x o y è NULL, alcuni confronti logici restituiscono un valore UNKNOWN anziché True o False.  
  
## <a name="sqlboolean-data-type"></a>Tipo di dati SqlBoolean  
 Lo spazio dei nomi `System.Data.SqlTypes` introduce un tipo `SqlBoolean` per rappresentare questa logica a 3 valori. I confronti tra gli spazi dei nomi `SqlTypes` restituiscono un tipo di valore `SqlBoolean`. Il valore UNKNOWN viene rappresentato dal valore Null del tipo `SqlBoolean`. Vengono fornite le proprietà `IsTrue`, `IsFalse` e `IsNull` per controllare il valore di un tipo `SqlBoolean`.  
  
## <a name="operations-functions-and-null-values"></a>Operazioni, funzioni e valori NULL  
 Tutti gli operatori aritmetici (+, -, \*, /, %), operatori bit per bit (~ &, e |), la maggior parte delle funzioni e restituiscono NULL se uno degli operandi o degli argomenti di `SqlTypes` sono NULL. La proprietà `IsNull` restituisce sempre un valore True o False.  
  
## <a name="precision"></a>Precisione  
 I valori massimi dei tipi di dati decimali CLR di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] sono diversi da quelli dei tipi di dati numerici e decimali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per i tipi di dati CLR decimali di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], inoltre, si presuppone la massima precisione. Nei tipi di dati CLR per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tuttavia, `SqlDecimal` fornisce la stessa scala e precisione massima e la stessa semantica del tipo di dati decimali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="overflow-detection"></a>Rilevamento dell'overflow  
 Nei tipi di dati CLR di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] è possibile che l'aggiunta di due numeri molto grandi non generi un'eccezione. Se invece non è stato utilizzato alcun operatore di controllo, il risultato restituito potrebbe essere un numero intero negativo. In `System.Data.SqlTypes` vengono generate eccezioni per tutti gli errori di overflow e underflow e per gli errori dovuti alla divisione per zero.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati di SQL Server in .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
