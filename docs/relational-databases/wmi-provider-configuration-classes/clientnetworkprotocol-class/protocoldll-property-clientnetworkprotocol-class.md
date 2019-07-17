---
title: Proprietà ProtocolDLL (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 31226e1a8e5c685dac971db1420d4ece489dfa02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040914"
---
# <a name="protocoldll-property-clientnetworkprotocol-class"></a>Proprietà ProtocolDLL (classe ClientNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Ottiene il nome del file con estensione dll richiesto dal protocollo di rete specificato dalla [configurazione di protocolli client](https://technet.microsoft.com/library/ms181035.aspx).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 A [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) che rappresenta il protocollo di rete utilizzato dal client di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore string che specifica il file con estensione dll del protocollo richiesto dal protocollo di rete del client.  
  
## <a name="remarks"></a>Note  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli di rete Client e le librerie di rete](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
