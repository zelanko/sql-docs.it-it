---
description: Metodo SetBoolValue (classe SqlServiceAdvancedProperty)
title: Metodo SetBoolValue (SqlServiceAdvancedProperty)
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetBoolValue Method (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetBoolValue method
ms.assetid: 5252b439-fce5-446a-8e57-99e3054bee69
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: db07b4e7dc83cffa60f5005195b9ac945620fe5b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427143"
---
# <a name="setboolvalue-method-sqlserviceadvancedproperty-class"></a>Metodo SetBoolValue (classe SqlServiceAdvancedProperty)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Imposta il valore booleano di una proprietà.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SetBoolValue [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlServiceAdvancedProperty](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) che rappresenta una proprietà avanzata.  
  
#### <a name="parameters"></a>Parametri  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*BoolValue*|Valore booleano che specifica il valore della proprietà avanzata.|  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Osservazioni  
 Il tipo di valore della proprietà deve essere booleano per impostare la proprietà su un valore booleano.  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
