---
description: Metodo SetNumericalValue (classe ClientNetworkProtocolProperty)
title: Metodo SetNumericalValue (ClientNetworkProtocolProperty)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetNumericalValue Method (ClientNetworkProtocolProperty
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetNumericalValue method
ms.assetid: d4d6df52-9e68-4003-9e28-ece6716ba7f1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ffdc80a3f2ca00b527ab5699429f20ff70c704c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460154"
---
# <a name="setnumericalvalue-method-clientnetworkprotocolproperty-class"></a>Metodo SetNumericalValue (classe ClientNetworkProtocolProperty)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Imposta il valore numerico della proprietà corrente a cui fa riferimento il valore della [proprietà PropertyIdx (classe ClientNetworkProtocolProperty)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SetNumericalValue [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 A [classe ClientNetworkProtocolProperty](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) che rappresenta un attributo del protocollo di rete utilizzato dal client di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
#### <a name="parameters"></a>Parametri  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*value*|Valore **uint32** che specifica il valore numerico della proprietà a cui si fa riferimento.|  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli client](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
