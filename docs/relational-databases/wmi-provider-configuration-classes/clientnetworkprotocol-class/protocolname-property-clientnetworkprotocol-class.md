---
description: Proprietà ProtocolName (classe ClientNetworkProtocol)
title: Proprietà ProtocolName (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolName Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolName property
ms.assetid: f8527121-fbcd-4d30-9b4a-1461149cb5a8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1323d4c47555bfebb717ba1627e6b4fc7c22c94b
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91888964"
---
# <a name="protocolname-property-clientnetworkprotocol-class"></a>Proprietà ProtocolName (classe ClientNetworkProtocol)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Ottiene il nome del protocollo di rete corrente specificato dalla [configurazione di protocolli client](../../../database-engine/configure-windows/configure-client-protocols.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.ProtocolName [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) che rappresenta il protocollo di rete utilizzato dal [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] client.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore stringa che specifica il nome del protocollo di rete del client corrente a cui fa riferimento il [Metodo SetOrderValue (classe ClientNetworkProtocol)](./setordervalue-method-clientnetworkprotocol-class.md).  
  
## <a name="remarks"></a>Commenti  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli di rete client e di librerie di rete](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
