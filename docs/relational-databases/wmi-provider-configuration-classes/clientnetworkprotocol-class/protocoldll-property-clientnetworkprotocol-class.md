---
description: Proprietà ProtocolDLL (classe ClientNetworkProtocol)
title: Proprietà ProtocolDLL (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolDLL Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolDLL property
ms.assetid: fe8650d5-7b9d-46f8-bf74-baf1d9d2a06a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6704808520b77867bd1a0b39af5118225398dae2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537285"
---
# <a name="protocoldll-property-clientnetworkprotocol-class"></a>Proprietà ProtocolDLL (classe ClientNetworkProtocol)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Ottiene il nome del file con estensione dll richiesto dal protocollo di rete specificato dalla [configurazione di protocolli client](https://technet.microsoft.com/library/ms181035.aspx).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) che rappresenta il protocollo di rete utilizzato dal [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] client.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore string che specifica il file con estensione dll del protocollo richiesto dal protocollo di rete del client.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli di rete client e di librerie di rete](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
