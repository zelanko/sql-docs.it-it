---
description: Metodo SetValue (classe ClientSettingsGeneralFlag)
title: Metodo SetValue (ClientSettingsGeneralFlag)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetValue Method (ClientSettingsGeneralFlag Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetValue method
ms.assetid: 34443689-a0e0-4668-a811-17532c6fd271
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ceab1e91f11cdb53ed157d595260b1fb448a453f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545302"
---
# <a name="setvalue-method-clientsettingsgeneralflag-class"></a>Metodo SetValue (classe ClientSettingsGeneralFlag)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Imposta tutti i valori del flag a cui si fa riferimento.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SetValue(Value)  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe ClientSettingsGeneralFlag](../../../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md) che rappresenta un flag generale per le impostazioni del server.  
  
#### <a name="parameters"></a>Parametri  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*Valore*|Valore booleano che specifica il valore del flag.|  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli client](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
