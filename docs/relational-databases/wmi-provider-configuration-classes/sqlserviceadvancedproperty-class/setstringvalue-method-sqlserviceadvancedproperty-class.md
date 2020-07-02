---
title: Metodo SetStringValue (classe SqlServiceAdvancedProperty)
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetStringValue Method (SqlServiceAdvancedProperty Class )
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStringValue method
ms.assetid: a02d05f6-1072-4709-9ecc-e23e51c8c898
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3a0f9b563d77a54fceeb58dbad0894582e5e4e8c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729147"
---
# <a name="setstringvalue-method-sqlserviceadvancedproperty-class-"></a>Metodo SetStringValue (classe SqlServiceAdvancedProperty)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Imposta il valore string di una proprietà.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SetStringValue(StrValue)  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlServiceAdvancedProperty](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) che rappresenta una proprietà avanzata.  
  
#### <a name="parameters"></a>Parametri  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*StrValue*|Valore string che specifica il valore della proprietà avanzata.|  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Osservazioni  
 Il tipo di valore della proprietà deve essere **String** per poter impostare la proprietà su un valore stringa.  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
