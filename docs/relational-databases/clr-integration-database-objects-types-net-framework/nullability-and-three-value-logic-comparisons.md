---
title: Supporto di valori null e confronti di logica a tre valori | Microsoft Docs
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
ms.openlocfilehash: e5dbdf757038abbf2c98d3987ee14a9cb9184a61
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081323"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Supporto dei valori Null e confronti di logica a tre valori
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se si ha familiarità con le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati, si noterà somiglianza nella semantica e la precisione nel **System.Data.SqlTypes** dello spazio dei nomi nel [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Esistono tuttavia alcune differenze, le più importanti delle quali sono illustrate nel presente argomento.  
  
## <a name="null-values"></a>Valori NULL  
 Una differenza importante tra i tipi di dati Common Language Runtime (CLR) nativi e i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste nel fatto che i primi non consentono valori NULL, mentre i secondi forniscono semantica NULL completa.  
  
 La presenza di valori NULL influisce sui confronti. Quando si confrontano due valori x e y, se x o y è NULL, alcuni confronti logici restituiscono un valore UNKNOWN anziché True o False.  
  
## <a name="sqlboolean-data-type"></a>Tipo di dati SqlBoolean  
 Il **System.Data.SqlTypes** dello spazio dei nomi presenta un **SqlBoolean** tipo per rappresentare questa logica a 3 valori. I confronti tra qualsiasi **SqlTypes** restituire una **SqlBoolean** tipo valore. Il valore sconosciuto è rappresentato dal valore null del **SqlBoolean** tipo. La proprietà **IsTrue**, **IsFalse**, e **IsNull** vengono forniti per controllare il valore di un **SqlBoolean** tipo.  
  
## <a name="operations-functions-and-null-values"></a>Operazioni, funzioni e valori NULL  
 Tutti gli operatori aritmetici (+, -, \*, /, %), operatori bit per bit (~ &, e |), la maggior parte delle funzioni e restituiscono NULL se uno degli operandi o degli argomenti dei **SqlTypes** sono NULL. Il **IsNull** proprietà restituisce sempre un valore true o false.  
  
## <a name="precision"></a>Precision  
 I valori massimi dei tipi di dati decimali CLR di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] sono diversi da quelli dei tipi di dati numerici e decimali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per i tipi di dati CLR decimali di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], inoltre, si presuppone la massima precisione. In CLR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tuttavia **SqlDecimal** fornisce la stessa precisione massima e scala e la stessa semantica di tipo di dati decimal in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="overflow-detection"></a>Rilevamento dell'overflow  
 Nei tipi di dati CLR di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] è possibile che l'aggiunta di due numeri molto grandi non generi un'eccezione. Se invece non è stato utilizzato alcun operatore di controllo, il risultato restituito potrebbe essere un numero intero negativo. Nelle **System.Data.SqlTypes**, vengono generate eccezioni per tutti i overflow e underflow errori e gli errori di divisione per zero.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati di SQL Server in .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
