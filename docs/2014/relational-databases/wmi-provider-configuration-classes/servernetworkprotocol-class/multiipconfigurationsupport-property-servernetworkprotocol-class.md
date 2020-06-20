---
title: Proprietà MultiIpConfigurationSupport (classe ServerNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 80401a607c9155451a869082162affcca401ebca
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059904"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>Proprietà MultiIpConfigurationSupport (classe ServerNetworkProtocol)
  Ottiene la proprietà booleana che specifica se più indirizzi IP sono supportati da un protocollo di rete del server.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object  
.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [Proprietà ProtocolName (classe ServerNetworkProtocol)](servernetworkprotocol-class.md) che rappresenta il protocollo di rete utilizzato dall'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore booleano che specifica se più indirizzi IP sono supportati dal protocollo di rete del server. `true` se più indirizzi IP sono supportati dal protocollo di rete del server; `false` se più indirizzi IP non sono supportati dal protocollo di rete del server.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione di protocolli di rete server e di librerie di rete](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
