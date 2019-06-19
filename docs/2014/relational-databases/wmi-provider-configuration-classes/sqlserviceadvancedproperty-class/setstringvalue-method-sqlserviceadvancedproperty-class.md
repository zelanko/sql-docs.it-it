---
title: Metodo SetStringValue (classe SqlServiceAdvancedProperty) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetStringValue Method (SqlServiceAdvancedProperty Class )
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStringValue method
ms.assetid: a02d05f6-1072-4709-9ecc-e23e51c8c898
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b0209f3d8e77cfe893a0e462fc9ccf3761da8dfa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62911393"
---
# <a name="setstringvalue-method-sqlserviceadvancedproperty-class-"></a>Metodo SetStringValue (classe SqlServiceAdvancedProperty)
  Imposta il valore string di una proprietà.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object  
.SetStringValue(  
StrValue  
)  
  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlServiceAdvancedProperty](sqlserviceadvancedproperty-class.md) che rappresenta una proprietà avanzata.  
  
#### <a name="parameters"></a>Parametri  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*StrValue*|Valore string che specifica il valore della proprietà avanzata.|  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore `uint32` che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Note  
 Il tipo di valore della proprietà deve essere `string` per potere impostare la proprietà su un valore string.  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
