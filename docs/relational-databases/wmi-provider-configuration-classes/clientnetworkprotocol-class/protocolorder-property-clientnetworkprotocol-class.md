---
description: Proprietà ProtocolOrder (classe ClientNetworkProtocol)
title: Proprietà ProtocolOrder (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolOrder Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 40ebe80960ca238cce4ff923a2e2457c45cd77f5
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91889197"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>Proprietà ProtocolOrder (classe ClientNetworkProtocol)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Ottiene il numero di ordine del protocollo di rete del client a cui si fa attualmente riferimento come specificato dal [metodo SetOrderValue (classe ClientNetworkProtocol)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) che rappresenta il protocollo di rete utilizzato dal [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] client.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore **uint32** che specifica il numero di ordine del protocollo di rete del client a cui si fa attualmente riferimento come impostato dal metodo **OrderValue** . Se il protocollo di rete client è disabilitato, questo valore sarà zero.  
  
## <a name="remarks"></a>Commenti  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare i protocolli client](../../../database-engine/configure-windows/configure-client-protocols.md)   
 [Configurazione di protocolli di rete client e di librerie di rete](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
