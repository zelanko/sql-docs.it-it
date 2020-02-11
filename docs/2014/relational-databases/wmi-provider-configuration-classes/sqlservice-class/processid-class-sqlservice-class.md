---
title: Classe ProcessId (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ProcessId Class (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProcessId property
ms.assetid: 99b5a2e9-b44a-48a0-993e-04bd15c7fef4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b9e6c04a0ae0000284f3550d39e47c973adbe8ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63061919"
---
# <a name="processid-class-sqlservice-class"></a>Classe ProcessId (classe SqlService)
  Ottiene l'ID di processo di sistema che identifica in modo univoco un servizio.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object  
.ProcessId [= value]  
```  
  
## <a name="parts"></a>Parti  
 *oggetto*  
 Oggetto della [classe SqlService](sqlservice-class.md) che rappresenta il servizio.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore `uint32` che specifica l'ID che identifica in modo univoco il processo.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="example"></a>Esempio  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
