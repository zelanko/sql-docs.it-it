---
title: Supporto dei valori null e confronti di logica a tre valori | Microsoft Docs
description: Questo articolo illustra il modo in cui i tipi di dati SQL Server differiscono dai tipi di System. Data. SqlTypes nel .NET Framework, che hanno semantica e precisione simili.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 3f016abf2113afef3e02f01fd9842b91b742d50a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488459"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Supporto dei valori Null e confronti di logica a tre valori
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se si ha familiarità con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i tipi di dati, si troveranno una semantica e una precisione simili nello spazio dei nomi **System. Data. SqlTypes** in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Esistono tuttavia alcune differenze, le più importanti delle quali sono illustrate nel presente argomento.  
  
## <a name="null-values"></a>Valori NULL  
 Una differenza importante tra i tipi di dati Common Language Runtime (CLR) nativi e i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste nel fatto che i primi non consentono valori NULL, mentre i secondi forniscono semantica NULL completa.  
  
 La presenza di valori NULL influisce sui confronti. Quando si confrontano due valori x e y, se x o y è NULL, alcuni confronti logici restituiscono un valore UNKNOWN anziché True o False.  
  
## <a name="sqlboolean-data-type"></a>Tipo di dati SqlBoolean  
 Lo spazio dei nomi **System. Data. SqlTypes** introduce un tipo **SqlBoolean** per rappresentare questa logica a 3 valori. I confronti tra qualsiasi **tipo SqlTypes** restituiscono un tipo di valore **SqlBoolean** . Il valore sconosciuto è rappresentato dal valore null del tipo **SqlBoolean** . Per controllare il valore di un tipo **SqlBoolean** vengono fornite le proprietà **IsTrue** **, IsTrue e** **IsNull** .  
  
## <a name="operations-functions-and-null-values"></a>Operazioni, funzioni e valori NULL  
 Tutti gli operatori aritmetici (+, \*-,,/,%), gli operatori bit per bit (~, & e |) e la maggior parte delle funzioni restituiscono null se uno degli operandi o degli argomenti di **SqlTypes** è null. La proprietà **IsNull** restituisce sempre un valore true o false.  
  
## <a name="precision"></a>Precision  
 I valori massimi dei tipi di dati decimali CLR di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] sono diversi da quelli dei tipi di dati numerici e decimali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per i tipi di dati CLR decimali di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], inoltre, si presuppone la massima precisione. In CLR per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tuttavia, **SqlDecimal** fornisce la stessa precisione e scala massima e la stessa semantica del tipo di dati Decimal in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="overflow-detection"></a>Rilevamento dell'overflow  
 Nei tipi di dati CLR di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] è possibile che l'aggiunta di due numeri molto grandi non generi un'eccezione. Se invece non è stato utilizzato alcun operatore di controllo, il risultato restituito potrebbe essere un numero intero negativo. In **System. Data. SqlTypes**vengono generate eccezioni per tutti gli errori di overflow e underflow e per gli errori di divisione per zero.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati di SQL Server in .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
