---
title: Metodo sedisable (classe ServerNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetDisable Method (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDisable method
ms.assetid: 0ebbe0c5-07ad-4a76-a918-e379930adf71
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3176227aba4de1e5aca1be35ec1f071a15caa49e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059855"
---
# <a name="setdisable-method-servernetworkprotocol-class"></a>Metodo SetDisable (classe ServerNetworkProtocol)
  Disabilita il protocollo di rete del server.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object  
.SetDisable()  
  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto [ServerNetworkProtocol Class] ServerNetworkProtocol-class.md) che rappresenta il protocollo di rete utilizzato dall'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore uint32 che è 0 se il servizio è stato modificato correttamente, 1 se la richiesta non è supportata e qualsiasi altro numero per indicare un errore.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli di rete server e di librerie di rete](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
