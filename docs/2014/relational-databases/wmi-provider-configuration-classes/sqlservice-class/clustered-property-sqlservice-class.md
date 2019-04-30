---
title: Proprietà (classe SqlService) in cluster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- Clustered Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Clustered property
ms.assetid: f714e7f5-c2db-45c6-9536-6ca2cb5b42aa
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 065440d834033d1c1c999ea9d38d321be9a6278c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63223327"
---
# <a name="clustered-property-sqlservice-class"></a>Proprietà Clustered (classe SqlService)
  Ottiene il valore della proprietà booleana che specifica se il servizio fa parte di un'istanza cluster.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object  
.Clustered [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlService](sqlservice-class.md) che rappresenta il servizio.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore booleano che specifica se il servizio fa parte di un'istanza cluster: `true` se il servizio fa parte di un'istanza cluster; `false` se il servizio non fa parte di un'istanza cluster.  
  
## <a name="remarks"></a>Note  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
