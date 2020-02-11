---
title: Proprietà ProtocolOrder (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ProtocolOrder Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0a0043e5a894e3f3f1b778a6f42fe6e3bacbbc78
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63192889"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>Proprietà ProtocolOrder (classe ClientNetworkProtocol)
  Ottiene il numero di ordine del protocollo di rete del client a cui si fa attualmente riferimento come specificato dal [metodo SetOrderValue (classe ClientNetworkProtocol)](clientnetworkprotocol-class.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object  
.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>Parti  
 *oggetto*  
 A [classe ClientNetworkProtocol](clientnetworkprotocol-class.md) che rappresenta il protocollo di rete utilizzato dal client di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore `uint32` che specifica il numero di ordine del protocollo di rete del client a cui si fa attualmente riferimento come impostato dal metodo `OrderValue`. Se il protocollo di rete client è disabilitato, questo valore sarà zero.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare i protocolli client](https://technet.microsoft.com/library/ms181035.aspx)   
 [Configurazione di protocolli di rete client e di librerie di rete](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
