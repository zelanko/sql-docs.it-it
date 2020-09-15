---
description: Metodo toString (DateTimeOffset)
title: Metodo toString (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 66931c3ada32b112de920aab3ac62fdb50fd40cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431433"
---
# <a name="tostring-method-datetimeoffset"></a>Metodo toString (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce una rappresentazione stringa dell'oggetto **DateTimeOffset**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Rappresentazione stringa dell'oggetto **DateTimeOffset**.  
  
## <a name="remarks"></a>Osservazioni  
 La stringa ha il formato `YYYY-MM-DD HH:mm:ss[.fffffff] [+|-]HH:mm`.  
  
 Nei secondi frazionari della stringa restituita vengono aggiunti zero alla precisione dichiarata. Ad esempio, un **datetimeoffset(6)** con il valore "2010-03-10 12:34:56.78-08:00" verrà formattato da DateTimeOffset.toString come "2010-03-10 12:34:56.780000 -08:00".  
  
## <a name="see-also"></a>Vedere anche  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membri di DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
