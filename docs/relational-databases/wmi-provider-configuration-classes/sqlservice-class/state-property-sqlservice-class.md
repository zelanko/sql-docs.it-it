---
description: Proprietà State (classe SqlService)
title: Proprietà state (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- State Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- State property
ms.assetid: 9e09f419-947c-4d4b-9a49-2d3396c847cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 606c991cd1f5b20f888fc2a2bf9d500e4e5ec410
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485077"
---
# <a name="state-property-sqlservice-class"></a>Proprietà State (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Ottiene o imposta lo stato corrente del servizio.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.State [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) che rappresenta il servizio.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore uint32 che specifica lo stato del servizio.  
  
 I valori possibili sono i seguenti:  
  
 1  
 Arrestato. Il servizio è stato arrestato.  
  
 2  
 In attesa dell'avvio. Il servizio è in attesa di essere avviato.  
  
 3  
 In attesa dell'arresto. Il servizio è in attesa di essere arrestato.  
  
 4  
 In esecuzione. Il servizio è in esecuzione.  
  
 5  
 In attesa della ripresa. Il servizio è in attesa di essere ripreso.  
  
 6  
 In attesa della sospensione. Il servizio è in attesa di essere sospeso.  
  
 7  
 (sospeso) Il servizio è in pausa.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
