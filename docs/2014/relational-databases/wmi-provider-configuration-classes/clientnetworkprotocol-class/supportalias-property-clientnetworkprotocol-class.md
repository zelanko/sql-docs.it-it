---
title: Proprietà SupportAlias (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SupportAlias Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SupportAlias property
ms.assetid: 1e7a2e87-c356-40a6-a6d9-e492467629f9
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d28ec166f8954b874f98b7f9f441280ab9064f1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62826757"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>Proprietà SupportAlias (classe ClientNetworkProtocol)
  Ottiene la proprietà booleana che specifica se il protocollo di rete corrente specificato dal [Metodo SetOrderValue (classe ClientNetworkProtocol)](clientnetworkprotocol-class.md) supporta gli alias.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object  
.SupportAlias [= value]  
```  
  
## <a name="parts"></a>Parti  
 *oggetto*  
 A [classe ClientNetworkProtocol](clientnetworkprotocol-class.md) che rappresenta il protocollo di rete utilizzato dal client di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore booleano che specifica se il protocollo di rete del client supporta gli alias.  
  
 Se True, il protocollo di rete del client supporta gli alias.  
  
 Se False, il protocollo di rete del client non supporta gli alias.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli client](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
