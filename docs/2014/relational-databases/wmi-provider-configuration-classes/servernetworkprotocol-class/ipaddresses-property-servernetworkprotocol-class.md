---
title: Proprietà IpAddresses (classe ServerNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- IpAddresses Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- IpAddresses property
ms.assetid: e5d66f7e-9719-436e-b723-12d56f914a05
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e7b2adf53bc6ebca14e2d3b4dc2cee248a4b6720
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63190296"
---
# <a name="ipaddresses-property-servernetworkprotocol-class"></a>Proprietà IpAddresses (classe ServerNetworkProtocol)
  Ottiene gli indirizzi IP associati al protocollo di rete del server.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object  
.IpAddresses [= value]  
```  
  
## <a name="parts"></a>Parti  
 *oggetto*  
 `ServerNetworkProtocol` Oggetto che rappresenta il protocollo di rete utilizzato dall'istanza di. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Matrice di oggetti della [classe ServerNetworkProtocolIPAdress](../servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) che rappresentano gli indirizzi IP supportati dal protocollo di rete del server.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedi anche  
 [Configurazione di protocolli di rete server e di librerie di rete](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
