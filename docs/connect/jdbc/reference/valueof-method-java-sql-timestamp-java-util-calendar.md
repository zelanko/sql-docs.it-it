---
title: Metodo valueOf (java.sql.Timestamp, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7320c383-0b06-446d-963b-7005e50324a2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 11d8f8e346fdb0f07770feec815e5aa5fe88355f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001581"
---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>Metodo valueOf (java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un oggetto **DateTimeOffset** che rappresenta un punto nel tempo in un particolare offset rispetto a GMT in base a un valore java.sql.Timestamp e un valore java.util.Calendar che indica l'offset.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, java.util.Calendar calendar)  
```  
  
#### <a name="parameters"></a>Parametri  
 *timestamp*  
  
 Valore java.sql.Timestamp.  
  
 *calendario*  
  
 Valori di offset.  I componenti di data e ora del *Calendario* verranno impostati in base al valore di *timestamp* .  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un oggetto DateTimeOffset che rappresenta il punto nel tempo specificato dall'oggetto Java. SQL. timestamp in corrispondenza del fuso orario dell'oggetto Java. util. Calendar specificato.  
  
## <a name="remarks"></a>Remarks  
 Questo metodo imposta inoltre l'oggetto Java. util. Calendar sul momento specificato dall'oggetto Java. SQL. timestamp.  
  
## <a name="see-also"></a>Vedere anche  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membri di DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
