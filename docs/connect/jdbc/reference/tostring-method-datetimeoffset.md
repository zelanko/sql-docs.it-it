---
title: Metodo ToString (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef3cd31068c324475e8edfe8bf8f7c16acc4a2de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968518"
---
# <a name="tostring-method-datetimeoffset"></a>Metodo toString (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce una rappresentazione di stringa dell'oggetto **DateTimeOffset** .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Rappresentazione di stringa dell'oggetto **DateTimeOffset** .  
  
## <a name="remarks"></a>Remarks  
 Il formato della stringa è *aaaa*-*mm*-*GG * * HH*:*mm*:*ss*[. *fffffff*] [+ |-]*HH*:*mm*.  
  
 Nei secondi frazionari della stringa restituita vengono aggiunti zero alla precisione dichiarata. Ad esempio, un **DateTimeOffset (6)** con un valore di "2010-03-10 12:34:56.78-08:00" verrà formattato da DateTimeOffset. ToString come "2010-03-10 12:34:56.780000-08:00".  
  
## <a name="see-also"></a>Vedere anche  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membri di DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
